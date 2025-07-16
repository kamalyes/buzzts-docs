<script setup lang="ts">
import { ref } from 'vue';
import { base64ToImageFile } from 'buzzts';

const base64 = ref('data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAAUAAAAFCAYAAACNbyblAAAAHElEQVR42mP8//8/w38GIAXD7Qh4AAAAAElFTkSuQmCC');
const file = ref<File | null>(null);

function convertToFile() {
  file.value = base64ToImageFile(base64.value);
}
</script>

<template>
  <n-card title="Base64 to File">
    <n-input v-model:value="base64" placeholder="输入 Base64 字符串" />
    <n-button type="primary" @click="convertToFile">转换为 File</n-button>
     <!-- File 信息展示 -->
    <n-space vertical v-if="file">
      <h4>File 信息:</h4>
      <n-text>名称: {{ file.name }}</n-text>
      <n-text>类型: {{ file.type }}</n-text>
      <n-text>大小: {{ file.size }} 字节</n-text>
      <n-text>最后修改日期: {{ file.lastModifiedDate ? new Date(file.lastModifiedDate).toLocaleString() : 'N/A' }}</n-text>
    </n-space>
  </n-card>
</template>
