<script setup lang="ts">
import { ref, computed } from "vue";
import { randColorHexShort } from "buzzts";

// HEX字符集，默认16进制字符
const hexChars = ref("0123456789abcdef");

// 生成结果，初始为null
const colorResult = ref<string | null>(null);

// 生成颜色函数，调用randColorHexShort并传入字符集
function generateColor() {
  colorResult.value = randColorHexShort(hexChars.value);
}

// 计算显示文本
const resultText = computed(() => {
  if (!colorResult.value) return "点击生成短格式HEX颜色";
  return `randColorHexShort() = ${colorResult.value}`;
});
</script>

<template>
  <n-card title="短格式HEX颜色生成">
    <n-space vertical>
      <n-input v-model:value="hexChars" label="HEX字符集" placeholder="请输入HEX字符集" />

      <n-button type="primary" @click="generateColor">生成颜色</n-button>

      <n-gradient-text type="info">{{ resultText }}</n-gradient-text>
      
      <span
        :style="{ 
          display: 'inline-block', 
          width: '40px', 
          height: '20px', 
          backgroundColor: colorResult && colorResult.includes('#') ? colorResult : 'transparent', 
          marginLeft: '10px', 
          border: '1px solid #ccc' 
        }"
      ></span>
    </n-space>
  </n-card>
</template>
