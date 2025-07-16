<script setup lang="ts">
import { ref } from 'vue';
import { urlToImageFile } from 'buzzts';

// 状态变量
const imageUrl = ref<string>(`${window.origin}/logo.svg`); // 图像 URL
const file = ref<File | null>(null); // File 对象
const error = ref<string | null>(null); // 错误信息
const fileUrl = ref<string | null>(null); // File URL

// 将图像 URL 转换为 File 的函数
async function convertToFile() {
  resetError(); // 在处理之前重置错误信息
  try {
    const fileName = 'image.png'; // 可以根据需要自定义文件名
    file.value = await urlToImageFile(imageUrl.value, fileName); // 调用转换函数
    if (file.value) {
      fileUrl.value = URL.createObjectURL(file.value); // 创建 File URL
      console.log('File URL:', fileUrl.value); // 调试信息
    } else {
      setError('未能创建有效的 File 对象'); // 错误处理
    }
  } catch (err) {
    setError((err as Error).message); // 捕获并设置错误信息
  }
}

// 重置组件状态的函数
function reset() {
  imageUrl.value = `${window.origin}/logo.svg`; // 重置为默认 URL
  file.value = null; // 清空 File
  resetError(); // 清除错误信息
  fileUrl.value = null; // 清除 File URL
}

// 重置错误状态的函数
function resetError() {
  error.value = null; // 清空错误信息
}

// 设置错误信息的函数
function setError(message: string) {
  error.value = message; // 设置错误信息
}

// 格式化日期的函数
function formatDate(timestamp: number): string {
  const date = new Date(timestamp);
  return date.toLocaleString(); // 按需格式化日期
}
</script>
<template>
  <n-card title="URL to Image File">
    <n-space vertical>
      <n-input v-model:value="imageUrl" placeholder="输入图像 URL" class="input" />
      <div>
        <n-button type="primary" @click="convertToFile" style="margin-right: 12px">转换为 File</n-button>
        <n-button type="primary" @click="reset">重置</n-button>
      </div>
    </n-space>

    <!-- File 信息展示 -->
    <n-space vertical v-if="file">
      <h4>File 信息:</h4>
      <n-text>名称: {{ file.name }}</n-text>
      <n-text>类型: {{ file.type }}</n-text>
      <n-text>大小: {{ file.size }} 字节</n-text>
      <n-text>最后修改时间: {{ formatDate(file.lastModified) }}</n-text>
      <h4>图像展示:</h4>
      <img v-if="fileUrl" :src="fileUrl" alt="Image Preview" class="image-preview" />
      <a v-if="fileUrl" :href="fileUrl" :download="file.name">下载</a>
    </n-space>

    <n-gradient-text v-if="error" type="info" style="margin-top: 12px; display: block;">
      {{ error }}
    </n-gradient-text>
  </n-card>
</template>
<style scoped>
.image-preview {
  max-width: 100%; /* 最大宽度为 100% */
  height: auto; /* 高度自适应 */
  margin-top: 10px; /* 上边距 */
}
</style>
