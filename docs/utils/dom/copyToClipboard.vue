<template>
    <n-card title="剪贴板操作">
      <n-space vertical>
        <n-input
          type="textarea"
          v-model:value="testClipboardText"
          placeholder="请输入测试文本内容"
          style="width: 100%;"
          :rows="3"
        />
        <n-space wrap>
          <h2></h2>
          <n-button type="primary" @click="copyText">复制文本</n-button>
          <n-button type="info" @click="getClipboardText">点击我获取剪贴板内容</n-button>
        </n-space>
        <n-gradient-text type="info"> {{ clipboardText }} </n-gradient-text>
      </n-space>
    </n-card>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import { getFromClipboard, copyToClipboard, randString, randInt, RandType } from 'buzzts';

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

// 复制文本的函数
const copyText = async () => {
  try {
    await copyToClipboard(testClipboardText.value);
    alert('复制成功');
  } catch (err) {
    console.error('复制失败:', err);
  }
};
</script>

<style scoped>
/* 可以添加样式以美化组件 */
</style>
