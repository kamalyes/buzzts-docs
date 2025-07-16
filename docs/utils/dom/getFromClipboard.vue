<template>
    <n-card title="剪贴板操作">
      <n-space vertical>
          <n-button type="info" @click="getClipboardText">复制任何内容后可点击我获取剪贴板内容</n-button>
        <n-gradient-text type="info"> {{ clipboardText }} </n-gradient-text>
      </n-space>
    </n-card>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import { getFromClipboard, randString, randInt, RandType } from 'buzzts';

// 使用 ref 创建响应式变量
const clipboardText = ref<string>('');
const testClipboardText = ref(randString(randInt(100,200),RandType.LOWERCASE| RandType.CAPITAL| RandType.NUMBER))

// 获取剪贴板内容的函数
const getClipboardText = async () => {
  try {
    clipboardText.value = await getFromClipboard();
  } catch (err) {
    console.error('读取失败:', err);
  }
};

</script>

<style scoped>
/* 可以添加样式以美化组件 */
</style>
