<template>
  <n-card title="URL to Image Blob">
    <n-space vertical>
      <n-input v-model:value="imageUrl" placeholder="输入图像 URL" class="input" />
      <div>
        <n-button type="primary" @click="convertToBlob" style="margin-right: 12px">转换为 Blob</n-button>
        <n-button type="primary" @click="reset">重置</n-button>
      </div>
    </n-space>

    <!-- Blob 信息展示 -->
    <n-space vertical v-if="blob">
      <h4>Blob 信息:</h4>
      <n-text>类型: {{ blob.type }}</n-text>
      <n-text>大小: {{ blob.size }} 字节</n-text>
      <h4>图像展示:</h4>
      <img :src="blobUrl" alt="Blob Image" class="image-preview" />
      <a :href="blobUrl" download="image.blob">下载</a>
    </n-space>

    <n-gradient-text v-if="error" type="info" style="margin-top: 12px; display: block;">
      {{ error }}
    </n-gradient-text>
  </n-card>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import { urlToImageBlob } from 'buzzts';

// 状态变量
const imageUrl = ref<string>(`${window.origin}/logo.svg`); // 图像 URL
const blob = ref<Blob | null>(null); // Blob 对象
const error = ref<string | null>(null); // 错误信息
const blobUrl = ref<string | null>(null); // Blob URL

// 将图像 URL 转换为 Blob 的函数
async function convertToBlob() {
  resetError(); // 在处理之前重置错误信息
  try {
    blob.value = await urlToImageBlob(imageUrl.value); // 调用转换函数
    blobUrl.value = URL.createObjectURL(blob.value); // 创建 Blob URL
  } catch (err) {
    setError((err as Error).message); // 捕获并设置错误信息
  }
}

// 重置组件状态的函数
function reset() {
  imageUrl.value = `${window.origin}/logo.svg`; // 重置为默认 URL
  blob.value = null; // 清空 Blob
  resetError(); // 清除错误信息
  blobUrl.value = null; // 清除 Blob URL
}

// 重置错误状态的函数
function resetError() {
  error.value = null; // 清空错误信息
}

// 设置错误信息的函数
function setError(message: string) {
  error.value = message; // 设置错误信息
}

// 格式化日期的函数（如果将来需要）
function formatDate(timestamp: number): string {
  const date = new Date(timestamp);
  return date.toLocaleString(); // 按需格式化日期
}
</script>

<style scoped>
.image-preview {
  max-width: 100%; /* 最大宽度为 100% */
  height: auto; /* 高度自适应 */
  margin-top: 10px; /* 上边距 */
}
</style>
