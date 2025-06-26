<script setup lang="ts">
import { ref } from 'vue';
import ColorRangeInput from './rangeInput.vue';
import { randColorHSL } from 'buzzts';

// H、S、L 范围，默认全范围
const hRange = ref<[number, number]>([0, 360]);
const sRange = ref<[number, number]>([0, 100]);
const lRange = ref<[number, number]>([0, 100]);

const colorResult = ref<string>('点击生成随机HSL颜色');

function generateRandColor() {
  colorResult.value = randColorHSL(hRange.value, sRange.value, lRange.value);
}
</script>

<template>
  <n-card title="随机HSL颜色生成">
    <n-space vertical>
      <ColorRangeInput label="色调范围 (H)" :min="0" :max="360" v-model:modelValue="hRange" />
      <ColorRangeInput label="饱和度范围 (S)" :min="0" :max="100" v-model:modelValue="sRange" />
      <ColorRangeInput label="亮度范围 (L)" :min="0" :max="100" v-model:modelValue="lRange" />

      <n-button type="primary" @click="generateRandColor">生成随机颜色</n-button>

      <div style="margin-top: 16px; font-weight: bold; font-size: 20px;">
        {{ colorResult }}
        <span
          :style="{ 
            display: 'inline-block', 
            width: '40px', 
            height: '20px', 
            backgroundColor: colorResult, 
            marginLeft: '10px', 
            border: '1px solid #ccc' 
          }"
        ></span>
      </div>
    </n-space>
  </n-card>
</template>
