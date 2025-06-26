<script setup lang="ts">
import { ref, computed } from "vue";
import { randBernoulli } from "buzzts";

const p = ref<number>(0.5);
const result = ref<boolean | null>(null);

function generateBernoulli() {
  result.value = randBernoulli(p.value);
}

const resultText = computed(() => {
  if (result.value === null) return "点击生成伯努利随机布尔值";
  return `randBernoulli() = ${result.value}`;
});
</script>

<template>
  <n-card title="伯努利分布随机布尔值">
    <n-space vertical>
      <n-input-number v-model:value="p" :min="0" :max="1" step="0.01" label="事件发生概率 p" />

      <n-button type="primary" @click="generateBernoulli">生成</n-button>

      <n-gradient-text type="info">{{ resultText }}</n-gradient-text>
    </n-space>
  </n-card>
</template>
