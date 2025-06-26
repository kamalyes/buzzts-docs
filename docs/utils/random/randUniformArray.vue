<script setup lang="ts">
import { ref, computed } from "vue";
import { randUniformArray } from "buzzts";

const length = ref<number>(5);
const min = ref<number>(0);
const max = ref<number>(1);
const result = ref<number[] | null>(null);

function generateArray() {
  result.value = randUniformArray(length.value, min.value, max.value);
}

const resultText = computed(() => {
  if (!result.value) return "点击生成均匀分布随机数组";
  return `randUniformArray(length=${length.value}, min=${min.value}, max=${max.value}) = [${result.value.map(v => v.toFixed(2)).join(", ")}]`;
});
</script>

<template>
  <n-card title="均匀分布随机数组生成">
    <n-space vertical>
      <n-input-number v-model:value="length" :min="1" label="数组长度" />
      <n-input-number v-model:value="min" label="最小值" />
      <n-input-number v-model:value="max" :min="min" label="最大值" />

      <n-button type="primary" @click="generateArray">生成随机数组</n-button>

      <n-gradient-text type="info">{{ resultText }}</n-gradient-text>
    </n-space>
  </n-card>
</template>
