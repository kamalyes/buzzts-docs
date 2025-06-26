<script setup lang="ts">
import { ref, computed } from 'vue';
import ColorRangeInput from './rangeInput.vue';
import { randColorCMYK } from 'buzzts';

// CMYK 四个通道范围
const cRange = ref<[number, number]>([0, 100]);
const mRange = ref<[number, number]>([0, 100]);
const yRange = ref<[number, number]>([0, 100]);
const kRange = ref<[number, number]>([0, 100]);

const cmykStr = ref<string | null>(null);
const rgbStr = ref<string>(''); // 转换后用于预览的 RGB

// CMYK 转 RGB，方便预览
function cmykToRgb(c: number, m: number, y: number, k: number) {
  const C = c / 100, M = m / 100, Y = y / 100, K = k / 100;
  const R = Math.round(255 * (1 - C) * (1 - K));
  const G = Math.round(255 * (1 - M) * (1 - K));
  const B = Math.round(255 * (1 - Y) * (1 - K));
  return `rgb(${R}, ${G}, ${B})`;
}

function generaterandColorCMYK() {
  cmykStr.value = randColorCMYK(cRange.value, mRange.value, yRange.value, kRange.value);
  if (cmykStr.value) {
    // 解析 cmykStr，格式假设为 "cmyk(10%, 20%, 30%, 40%)"
    const match = cmykStr.value.match(/cmyk\((\d+)%?,\s*(\d+)%?,\s*(\d+)%?,\s*(\d+)%?\)/i);
    if (match) {
      const c = Number(match[1]);
      const m = Number(match[2]);
      const y = Number(match[3]);
      const k = Number(match[4]);
      rgbStr.value = cmykToRgb(c, m, y, k);
    } else {
      rgbStr.value = '';
    }
  }
}
</script>

<template>
  <n-card title="随机CMYK颜色生成">
    <n-space vertical>
      <ColorRangeInput label="青色范围 (C)" :min="0" :max="100" v-model:modelValue="cRange" />
      <ColorRangeInput label="品红范围 (M)" :min="0" :max="100" v-model:modelValue="mRange" />
      <ColorRangeInput label="黄色范围 (Y)" :min="0" :max="100" v-model:modelValue="yRange" />
      <ColorRangeInput label="黑色范围 (K)" :min="0" :max="100" v-model:modelValue="kRange" />

      <n-button type="primary" @click="generaterandColorCMYK">生成随机颜色</n-button>

      <div style="margin-top: 16px; font-weight: bold; font-size: 20px;">
        {{ cmykStr ?? '点击生成CMYK颜色' }}
        <span
          :style="{
            display: 'inline-block',
            width: '40px',
            height: '20px',
            backgroundColor: rgbStr,
            marginLeft: '10px',
            border: '1px solid #ccc'
          }"
        ></span>
      </div>
    </n-space>
  </n-card>
</template>
