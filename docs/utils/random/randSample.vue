<script setup lang="ts">
import { ref, computed } from "vue";
import { randSample, rangeWithStep, randUniqueSample } from "buzzts";

// 先用 rangeWithStep 生成数字数组，再转成字符串初始化arrayText
const initialArray = randUniqueSample(rangeWithStep(-300, -20, 1), 10);
const arrayText = ref<string>(initialArray.join(","));

const n = ref<number>(2);
const result = ref<any[] | null>(null);

function generateSample() {
  const arr = arrayText.value.split(",").map(s => s.trim());
  if (n.value < 0) {
    result.value = ["错误：抽样数量不能为负"];
    return;
  }
  result.value = randSample(arr, n.value);
}

const resultText = computed(() => {
  if (!result.value) return "点击随机抽样";
  return `randSample([${arrayText.value}],${n.value}) = [${result.value.join(", ")}]`;
});
</script>

<template>
  <n-card title="随机抽样（允许重复）">
    <n-space vertical>
      <n-input v-model:value="arrayText" label="源数组 (逗号分隔)" />
      <n-input-number v-model:value="n" :min="0" label="抽样数量" />

      <n-button type="primary" @click="generateSample">抽样</n-button>

      <n-gradient-text type="info">{{ resultText }}</n-gradient-text>
    </n-space>
  </n-card>
</template>
