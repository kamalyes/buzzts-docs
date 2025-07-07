<script setup lang="ts">
import { ref, watch, computed } from 'vue';
import { timestampToDate } from 'buzzts';

const inputTs = ref<string | number>('1687497600');
const resultDate = ref<Date | null>(null);

// 使用 computed 生成结果文本
const resultText = computed(() => {
 const res = timestampToDate(inputTs.value);
  resultDate.value = res;
  if (resultDate.value === null) return "请输入有效时间戳";
  return `timestampToDate(${inputTs.value})=${resultDate.value.toISOString()}`;
});
</script>

<template>
  <n-card>
    <h3>时间戳转换器</h3>
    <n-input
      v-model:value="inputTs"
      placeholder="输入秒或毫秒时间戳"
      style="width: 100%; margin-bottom: 12px;"
    />
    <n-gradient-text type="info">{{ resultText }}</n-gradient-text>
  </n-card>
</template>

<style scoped>
</style>
