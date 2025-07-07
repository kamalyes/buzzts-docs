<script setup lang="ts">
import { ref, computed } from 'vue';
import { diffDaysWithDecimal } from 'buzzts';

// 解析日期工具，支持字符串或 Date
function parseDate(date: string | Date | null): Date | null {
  if (!date) return null;
  if (date instanceof Date) return isNaN(date.getTime()) ? null : date;
  const d = new Date(date);
  return isNaN(d.getTime()) ? null : d;
}

const dateA = ref<string>('2023-06-23');
const dateB = ref<string>('2023-06-20');

const daysDiff = computed(() => {
  const parsedA = parseDate(dateA.value);
  const parsedB = parseDate(dateB.value);
  if (!parsedA || !parsedB) return null;
  return diffDaysWithDecimal(parsedA, parsedB);
});

const resultText = computed(() => {
  if (daysDiff.value === null) return '日期无效，请重新输入';
  return `diffDaysWithDecimal(${dateA.value}, ${dateB.value}) = ${daysDiff.value} 天`;
});
</script>

<template>
  <div>
    <n-space align="center" style="width: 100%;">
      <n-date-picker
        v-model:value="dateA"
        type="datetime"
        placeholder="请选择日期A"
        style="width: 200px;"
        clearable
      />
      <n-date-picker
        v-model:value="dateB"
        type="datetime"
        placeholder="请选择日期B"
        style="width: 200px;"
        clearable
      />
      <!-- 计算按钮可去掉，计算自动触发 -->
    </n-space>
    <n-gradient-text type="info" style="margin-top: 12px;">{{ resultText }}</n-gradient-text>
  </div>
</template>
