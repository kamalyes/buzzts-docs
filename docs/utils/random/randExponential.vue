<script setup lang="ts">
import { ref, computed } from "vue";
import { randExponential } from "buzzts";

const lambda = ref<number>(1.5);
const result = ref<number | null>(null);

function generateExponential() {
  if (lambda.value <= 0) {
    result.value = null;
    return;
  }
  result.value = randExponential(lambda.value);
}

const resultText = computed(() => {
  if (result.value === null) return "点击生成指数分布随机数";
  return `randExponential() = ${result.value.toFixed(4)}`;
});
</script>

<template>
  <n-card title="指数分布随机数生成">
    <n-space vertical>
      <n-input-number v-model:value="lambda" :min="0.0001" label="λ (正数)" />

      <n-button type="primary" @click="generateExponential">生成</n-button>

      <n-gradient-text type="info">{{ resultText }}</n-gradient-text>
    </n-space>
  </n-card>
</template>
