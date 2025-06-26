<script setup lang="ts">
import { ref, computed } from 'vue';
import { randColorHEX } from 'buzzts';

const colorResult = ref<string | null>(null);

function generateRandColorHEX() {
  colorResult.value = randColorHEX();
}

const resultText = computed(() => {
  if (!colorResult.value) return '点击生成随机HEX颜色';
  return colorResult.value;
});
</script>

<template>
  <n-card title="随机HEX颜色生成">
    <n-space vertical>
      <n-button type="primary" @click="generateRandColorHEX">生成随机HEX颜色</n-button>

      <div style="margin-top: 16px; font-weight: bold; font-size: 20px; display: flex; align-items: center;">
        <span>{{ resultText }}</span>
        <span
          :style="{ 
            display: 'inline-block', 
            width: '40px', 
            height: '20px', 
            backgroundColor: colorResult?.includes('#') ? colorResult : 'transparent', 
            marginLeft: '10px', 
            border: '1px solid #ccc' 
          }"
        ></span>
      </div>
    </n-space>
  </n-card>
</template>
