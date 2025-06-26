<script setup lang="ts">
import { ref, computed } from "vue";
import { randPoisson } from "buzzts";

const lambda = ref<number>(3);
const result = ref<number | null>(null);

function generatePoisson() {
  if (lambda.value <= 0) {
    result.value = null;
    return;
  }
  result.value = randPoisson(lambda.value);
}

const resultText = computed(() => {
  if (result.value === null) return "点击生成泊松分布随机数";
  return `randPoisson() = ${result.value}`;
});
</script>

<template>
  <n-card title="泊松分布随机数生成">
    <n-space vertical>
      <n-input-number v-model:value="lambda" :min="0.0001" label="λ (平均事件数)" />

      <n-button type="primary" @click="generatePoisson">生成</n-button>

      <n-gradient-text type="info">{{ resultText }}</n-gradient-text>
    </n-space>
  </n-card>
</template>
