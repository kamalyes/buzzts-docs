<script setup lang="ts">
import { ref, computed } from 'vue';
import { getDayOfWeek } from 'buzzts';

const inputDate = ref<string>('2023-06-23');

const result = computed(() => {
  try {
    const res = getDayOfWeek(inputDate.value);
    // 这里假设无效日期会抛错或返回特殊值，您可根据实际调整
    if (typeof res !== 'number' || isNaN(res)) return null;
    return res;
  } catch {
    return null;
  }
});

const resultText = computed(() => {
  if (result.value === null) return "输入日期无效，请重新输入";
  return `getDayOfWeek(${inputDate.value}) = ${result.value}`;
});
</script>

<template>
  <div>
    <n-space align="center" style="width: 100%;">
      <n-date-picker
        v-model:value="inputDate"
        type="date"
        placeholder="请选择日期"
        style="width: 200px;"
        clearable
      />
    </n-space>
    <n-gradient-text type="info">{{ resultText }}</n-gradient-text>
  </div>
</template>
