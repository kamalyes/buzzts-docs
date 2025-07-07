<script setup lang="ts">
import { ref, computed } from 'vue';
import { compareTwoDates } from 'buzzts';

const dateA = ref<string | null>('2025-07-08 01:01:01');
const dateB = ref<string | null>('2025-07-10 01:01:01');
const comparisonType = ref<'before' | 'after'>('before');
const comparisonResult = computed(() => {
  if (dateA.value && dateB.value) {
    return compareTwoDates(dateA.value, dateB.value, comparisonType.value);
  }
  return null;
});

const resultText = computed(() => {
  return `compareTwoDates(${dateA.value}, ${dateB.value}, ${comparisonType.value}) = ${comparisonResult.value}`;
});
</script>

<template>
  <n-card>
    <h3>比较两个日期</h3>
    <n-date-picker v-model:value="dateA" placeholder="选择第一个日期" clearable style="width: 100%; margin-bottom: 12px;" />
    <n-date-picker v-model:value="dateB" placeholder="选择第二个日期" clearable style="width: 100%; margin-bottom: 12px;" />
    <n-select v-model:value="comparisonType" :options="[{ label: '早于', value: 'before' }, { label: '晚于', value: 'after' }]" style="margin-bottom: 12px;" />
    <n-gradient-text type="info">{{ resultText }}</n-gradient-text>
  </n-card>
</template>

<style scoped>
</style>
