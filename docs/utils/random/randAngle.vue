<script setup lang="ts">
import { ref, computed } from "vue";
import { randAngle } from "buzzts";

const result = ref<number | null>(null);

function generateAngle() {
  result.value = randAngle();
}

const resultText = computed(() => {
  if (result.value === null) return "点击生成随机角度";
  return `randAngle() = ${result.value.toFixed(2)}°`;
});
</script>

<template>
  <n-card title="随机角度生成">
    <n-space vertical>
      <n-button type="primary" @click="generateAngle">生成角度</n-button>

      <n-gradient-text type="info">{{ resultText }}</n-gradient-text>
    </n-space>
  </n-card>
</template>
