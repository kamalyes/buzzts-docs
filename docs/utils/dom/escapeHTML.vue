<template>
  <n-card title="转义HTML特殊字符">
    <n-space vertical>
      <n-input
        v-model:value="unsafeString"
        placeholder="输入需要转义的字符串"
        style="width: 100%;"
      />
      <n-button type="primary" @click="escapeString">转义</n-button>
      <n-gradient-text type="info" v-if="escapedString !== ''">
        转义后的字符串: {{ escapedString }}
      </n-gradient-text>
      <n-text v-else style="margin-top: 12px;">转义后的字符串为空</n-text>
    </n-space>
  </n-card>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import { escapeHTML } from 'buzzts';

// 定义响应式变量
const unsafeString = ref('This is a test & < > " \' ');
const escapedString = ref('');

// 转义字符串的函数
const escapeString = () => {
  escapedString.value = escapeHTML(unsafeString.value);
};
</script>

<style scoped>
/* 添加一些样式（可选） */
</style>
