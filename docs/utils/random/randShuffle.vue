<script setup lang="ts">
import { ref, computed } from "vue";
import { randShuffle, rangeWithStep, randUniqueSample } from "buzzts";

// 先用 rangeWithStep 生成数字数组，再转成字符串初始化arrayText
const initialArray = randUniqueSample(rangeWithStep(100, 200, 1), 20);
const arrayText = ref<string>(initialArray.join(","));

const result = ref<any[] | null>(null);

function generateShuffle() {
  const arr = arrayText.value.split(",").map(s => s.trim());
  result.value = randShuffle(arr);
}

const resultText = computed(() => {
  if (!result.value) return "点击数组洗牌";
  return `randShuffle([${arrayText.value}]) = [${result.value.join(", ")}]`;
});
</script>

<template>
  <n-card title="数组随机洗牌">
    <n-space vertical>
      <n-input v-model:value="arrayText" label="待打乱数组 (逗号分隔)" />

      <n-button type="primary" @click="generateShuffle">洗牌</n-button>

      <n-gradient-text type="info">{{ resultText }}</n-gradient-text>
    </n-space>
  </n-card>
</template>
