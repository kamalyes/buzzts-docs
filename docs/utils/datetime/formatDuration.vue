<script setup lang="ts">
import { ref, computed } from 'vue';
import { formatDuration } from 'buzzts'; // 确保正确引入

const durationSeconds = ref(5016); // 默认测试数据

// 计算属性用于生成格式化的持续时间结果文本
const resultText = computed(() => {
  const formattedDuration = formatDuration(durationSeconds.value);
  if (!formattedDuration) return "请先输入有效的秒数";
  return `formatDuration(${durationSeconds.value}) = ${formattedDuration}`;
});
</script>

<template>
  <n-space align="center" style="width: 100%;">
    <n-form-item label="格式化持续时间">
      <n-input type="number" v-model:value="durationSeconds" placeholder="输入秒数" />
    </n-form-item>
  </n-space>
  <n-gradient-text type="info">{{ resultText }}</n-gradient-text>
</template>

<style scoped>
/* 你可以在这里添加额外的样式 */
</style>
