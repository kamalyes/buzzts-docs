
<script setup lang="ts">
import { ref, computed } from 'vue';
import { getUnixTimestamp } from 'buzzts';

const inputDate = ref<string | Date>('2025-07-03 08:00:00');
const timestamp = ref<number | null>(null);

const resultText = computed(() => {
  const res = getUnixTimestamp(inputDate.value);
  timestamp.value = res;
  if (timestamp.value === null) return "输入日期无效，请重新输入";
  return `getUnixTimestamp(${inputDate.value}) = ${timestamp.value}`;
});

</script>
<template>
  <n-card>
    <h3>Unix 时间戳计算器</h3>
    <n-date-picker v-model:value="inputDate" type="datetime" clearable style="width: 100%; margin-bottom: 12px;" />
    <n-gradient-text type="info">{{ resultText }}</n-gradient-text>
  </n-card>
</template>

<style scoped>
</style>
