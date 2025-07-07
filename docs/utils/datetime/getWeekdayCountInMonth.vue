<script setup lang="ts">
import { ref, computed, watchEffect } from 'vue';
import { getWeekdayCountInMonth, WeekdayCount } from 'buzzts';

const date = ref('2025-07');

const weekdayCount = ref<WeekdayCount>({
  sunday: 0,
  monday: 0,
  tuesday: 0,
  wednesday: 0,
  thursday: 0,
  friday: 0,
  saturday: 0,
});

// 使用 watchEffect 来监视 date 的变化
watchEffect(() => {
  weekdayCount.value = getWeekdayCountInMonth(date.value) || {
    sunday: 0,
    monday: 0,
    tuesday: 0,
    wednesday: 0,
    thursday: 0,
    friday: 0,
    saturday: 0,
  };
});

const resultText = computed(() => {
  return `getWeekdayCountInMonth(${date.value}) = ${JSON.stringify(weekdayCount.value)}`;
});

// 星期几的名称数组
const weekdays = [
  { name: '周日', key: 'sunday' },
  { name: '周一', key: 'monday' },
  { name: '周二', key: 'tuesday' },
  { name: '周三', key: 'wednesday' },
  { name: '周四', key: 'thursday' },
  { name: '周五', key: 'friday' },
  { name: '周六', key: 'saturday' },
];
</script>

<template>
  <n-card title="计算某月每个星期几出现次数">
    <n-input v-model:value="date" style="width: 100%; margin-bottom: 16px;" />
    <n-gradient-text type="info">{{ resultText }}</n-gradient-text>
    <n-grid cols="2" x-gap="16" y-gap="12">
      <template v-for="weekday in weekdays" :key="weekday.key">
        <n-grid-item>{{ weekday.name }}</n-grid-item>
        <n-grid-item>{{ weekdayCount[weekday.key] ?? 0 }}</n-grid-item>
      </template>
    </n-grid>
  </n-card>
</template>
