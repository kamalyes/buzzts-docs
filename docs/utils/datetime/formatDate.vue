<script setup lang="ts">
import { ref, computed } from 'vue';
import { formatDate } from 'buzzts'; // 确保正确引入

const dateFormat = ref('YYYY-MM-DD');

// 计算属性用于生成格式化的日期结果文本
const resultText = computed(() => {
  const formattedDate = formatDate(dateFormat.value, new Date());
  if (!formattedDate) return "请先输入有效的日期格式";
  return `formatDate(${dateFormat.value}) = ${formattedDate}`;
});
</script>

<template>
  <n-space align="center" style="width: 100%;">
    <n-form-item label="格式化日期">
      <n-input v-model:value="dateFormat" placeholder="输入格式，例如 'YYYY-MM-DD'" />
    </n-form-item>
  </n-space>
  <n-gradient-text type="info">{{ resultText }}</n-gradient-text>
</template>

<style scoped>
/* 你可以在这里添加额外的样式 */
</style>
