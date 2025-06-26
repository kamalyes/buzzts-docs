<script setup lang="ts">
import { ref } from 'vue';
import ColorRangeInput from './rangeInput.vue';
import { randColorRGB } from 'buzzts';

const rRange = ref<[number, number]>([0, 255]);
const gRange = ref<[number, number]>([0, 255]);
const bRange = ref<[number, number]>([0, 255]);

const colorResult = ref<string>('点击生成随机颜色');

function generateRandColor() {
  colorResult.value = randColorRGB(rRange.value, gRange.value, bRange.value);
}
</script>

<template>
  <n-card title="随机RGB颜色生成">
    <n-space vertical>
      <ColorRangeInput label="红色范围" :min="0" :max="255" v-model:modelValue="rRange" />
      <ColorRangeInput label="绿色范围" :min="0" :max="255" v-model:modelValue="gRange" />
      <ColorRangeInput label="蓝色范围" :min="0" :max="255" v-model:modelValue="bRange" />

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
