<script setup lang="ts">
import { ref } from 'vue';
import { base64ToImageBlob } from 'buzzts';

const base64 = ref('data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAAUAAAAFCAYAAACNbyblAAAAHElEQVR42mP8//8/w38GIAXD7Qh4AAAAAElFTkSuQmCC');
const blob = ref<Blob | null>(null);

function convertToBlob() {
  blob.value = base64ToImageBlob(base64.value);
}
</script>
<template>
  <n-card title="Base64 to Blob">
    <n-input v-model:value="base64" placeholder="输入 Base64 字符串" />
    <n-button type="primary" @click="convertToBlob">转换为 Blob</n-button>
     <n-space vertical v-if="blob">
      <h4>Blob 信息:</h4>
      <n-text>类型: {{ blob.type }}</n-text>
      <n-text>大小: {{ blob.size }} 字节</n-text>
    </n-space>
  </n-card>
</template>
