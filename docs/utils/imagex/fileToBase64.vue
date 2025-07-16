<script setup lang="ts">
import { ref, onMounted } from 'vue';
import { fileToBase64 } from 'buzzts';

const base64 = ref<string | null>(null); // Base64 字符串
const errMsg = ref<string | null>(null); // 错误信息
const canvasRef = ref<HTMLCanvasElement | null>(null); // Canvas 引用

// 清空错误信息
const resetError = () => {
  errMsg.value = null;
};

// 设置错误信息
const setError = (message: string) => {
  errMsg.value = message;
};

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

// 将 Canvas 转换为 Base64
const generateBase64FromCanvas = async () => {
  const canvas = canvasRef.value;
  if (!canvas) {
    setError('Canvas 未找到');
    return;
  }

  // 将 Canvas 导出为 Blob
  canvas.toBlob(async (blob) => {
    if (!blob) {
      setError('无法生成 Blob');
      return;
    }

    // 创建 File 对象
    const file = new File([blob], 'canvas-image.png', { type: 'image/png' });

    try {
      // 使用 fileToBase64 方法将 File 转换为 Base64
      const base64String = await fileToBase64(file);
      base64.value = base64String;
    } catch (error) {
      setError((error as Error).message);
    }
  }, 'image/png');
};

// 处理绘制和转换为 Base64
const drawAndConvertToBase64 = async () => {
  resetError(); // 清空错误信息
  drawRandomShapes(); // 重新绘制图形
  await generateBase64FromCanvas(); // 生成 Base64
};

// 在组件挂载时绘制初始图形
onMounted(() => {
  drawRandomShapes();
});
</script>

<template>
  <n-card title="随机绘制图形">
    <n-space vertical>
      <canvas ref="canvasRef" width="60" height="60" style="border: 1px solid #ccc;"></canvas>
      <div>
        <n-button type="primary" @click="drawAndConvertToBase64" style="margin-right: 12px">随机绘制并转换为 Base64</n-button>
      </div>
    </n-space>
    <n-gradient-text v-if="errMsg" type="info" style="margin-top: 12px;">
      {{ errMsg }}
    </n-gradient-text>
    <n-gradient-text v-if="base64" type="info" style="margin-top: 12px;">
      Base64: {{ base64 }}
    </n-gradient-text>
  </n-card>
</template>

<style scoped>
/* 可以在这里添加样式 */
</style>
