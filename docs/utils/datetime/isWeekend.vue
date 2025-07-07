<script setup lang="ts">
import { ref, computed } from 'vue';
import { isWeekend } from 'buzzts';

const weekendDate = ref<string | null>('2025-07-08 01:01:01');
const isWeekendResult = computed(() => {
  return weekendDate.value ? isWeekend(weekendDate.value) : null;
});

const resultText = computed(() => {
  return `isWeekend(${weekendDate.value}}) = ${isWeekendResult.value}`;
});

</script>

<template>
  <n-card>
    <h3>判断日期是否为周末</h3>
    <n-date-picker v-model:value="weekendDate" placeholder="选择日期" clearable style="width: 100%; margin-bottom: 12px;" />
    <n-gradient-text type="info">{{ resultText }}</n-gradient-text>
  </n-card>
</template>

<style scoped>
</style>
