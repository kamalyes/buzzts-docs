<script setup lang="ts">
import { ref, computed } from "vue";
import { randBinomial } from "buzzts";

const n = ref<number>(10);
const p = ref<number>(0.5);
const result = ref<number | null>(null);

function generateBinomial() {
  if (n.value < 0 || p.value < 0 || p.value > 1) {
    result.value = null;
    return;
  }
  result.value = randBinomial(n.value, p.value);
}

const resultText = computed(() => {
  if (result.value === null) return "点击生成二项分布随机数";
  return `randBinomial() = ${result.value}`;
});
</script>

<template>
  <n-card title="二项分布随机数生成">
    <n-space vertical>
      <n-input-number v-model:value="n" :min="0" label="试验次数 n" />
      <n-input-number v-model:value="p" :min="0" :max="1" step="0.01" label="单次成功概率 p" />

      <n-button type="primary" @click="generateBinomial">生成</n-button>

      <n-gradient-text type="info">{{ resultText }}</n-gradient-text>
    </n-space>
  </n-card>
</template>
