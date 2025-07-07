<script setup lang="ts">
import { ref, computed } from 'vue';
import { isBetween } from 'buzzts';

const targetDate = ref<string | null>('2025-07-08 01:01:01');
const startDate = ref<string | null>('2025-07-11 01:01:01');
const endDate = ref<string | null>('2025-07-30 01:01:01');

const isInBetween = computed(() => {
  if (targetDate.value && startDate.value && endDate.value) {
    return isBetween(targetDate.value, startDate.value, endDate.value);
  }
  return null;
});

const resultText = computed(() => {
  return `isBetween(${targetDate.value}, ${startDate.value}, ${endDate.value}) = ${isInBetween.value}`;
});

</script>

<template>
  <n-card>
    <h3>判断目标日期是否在区间内</h3>
    <n-date-picker v-model:value="targetDate" placeholder="目标日期" clearable style="width: 100%; margin-bottom: 12px;" />
    <n-date-picker v-model:value="startDate" placeholder="起始日期" clearable style="width: 100%; margin-bottom: 12px;" />
    <n-date-picker v-model:value="endDate" placeholder="结束日期" clearable style="width: 100%; margin-bottom: 12px;" />
    <n-gradient-text type="info">{{ resultText }}</n-gradient-text>
  </n-card>
</template>

<style scoped>
</style>
