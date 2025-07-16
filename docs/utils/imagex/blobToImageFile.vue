<script setup lang="ts">
import { ref, onMounted } from 'vue';
import { blobToImageFile } from 'buzzts';

const blob = ref<Blob | null>(null);
const file = ref<File | null>(null);
const canvasRef = ref<HTMLCanvasElement | null>(null);

// 随机生成颜色
const getRandomColor = (): string => {
  return `hsl(${Math.random() * 360}, 100%, 50%)`;
};

// 随机绘制图形
const drawRandomShapes = () => {
  const canvas = canvasRef.value;
  if (!canvas) return;

  const ctx = canvas.getContext('2d');
  if (!ctx) return;

  // 清空画布
  ctx.clearRect(0, 0, canvas.width, canvas.height);

  // 随机绘制一些矩形和圆形
  for (let i = 0; i < 5; i++) {
    const x = Math.random() * canvas.width;
    const y = Math.random() * canvas.height;
    const size = Math.random() * 5 + 20; // 随机大小

    // 绘制矩形
    ctx.fillStyle = getRandomColor();
    ctx.fillRect(x, y, size, size);

    // 绘制圆形
    ctx.beginPath();
    ctx.arc(x + size / 2, y + size / 2, size / 2, 0, Math.PI * 2);
    ctx.fill();
  }
};

// 将 Canvas 转换为 Blob
const generateBlobFromCanvas = () => {
  const canvas = canvasRef.value;
  if (!canvas) return;

  canvas.toBlob((generatedBlob) => {
    if (generatedBlob) {
      blob.value = generatedBlob; // 设置 Blob
    }
  }, 'image/png');
};

// 将 Blob 转换为 File
const convertToFile = () => {
  // 重新绘制图形并生成新的 Blob
  drawRandomShapes();
  generateBlobFromCanvas();
  if (blob.value) {
    file.value = blobToImageFile(blob.value);
  }
};

// 在组件挂载时绘制初始图形并生成 Blob
onMounted(() => {
  drawRandomShapes();
  generateBlobFromCanvas();
});
</script>

<template>
  <n-card title="Blob to File">
    <canvas ref="canvasRef" width="60" height="60" style="border: 1px solid #ccc;"></canvas>
    <n-button type="primary" @click="convertToFile" style="margin-top: 12px;">随机绘制并转换为 File</n-button>
    <n-space vertical v-if="file">
      <h4>File 信息:</h4>
      <n-text>名称: {{ file.name }}</n-text>
      <n-text>类型: {{ file.type }}</n-text>
      <n-text>大小: {{ file.size }} 字节</n-text>
      <n-text>最后修改日期: {{ file.lastModifiedDate ? new Date(file.lastModifiedDate).toLocaleString() : 'N/A' }}</n-text>
    </n-space>
  </n-card>
</template>

<style scoped>
/* 可以在这里添加样式 */
</style>
