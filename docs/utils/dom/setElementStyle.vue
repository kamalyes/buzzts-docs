<template>
  <n-card vertical title="设置元素样式">
    <n-input
      type="textarea"
      v-model:value="defaultAfterStyle"
      :placeholder="`输入样式（${defaultAfterStyle}）`"
      style="width: 300px; margin-bottom: 10px;"
      :rows="3"
      @input="updateStyle"
    />
    <n-card>
      <n-button type="primary" @click="setRandomStyle">随机生成样式</n-button>
      <div id="target" :style="defaultAfterStyle"></div>
    </n-card>
  </n-card>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import { randInt, setElementStyle, randColorHEX } from 'buzzts';

// 定义响应式变量，设置更丰富的默认样式
const defaultAfterStyle = ref(`width: 150px; height: 150px; background: lightblue; margin-top: ${randInt(10,20)}px;`);

// 更新样式
const updateStyle = () => {
  const target = document.getElementById('target');
  if (target) {
    const styles = parseStyleString(defaultAfterStyle.value);
    setElementStyle(target, styles);
  }
};

// 定义随机生成样式的函数
const setRandomStyle = () => {
  defaultAfterStyle.value = `width: ${randInt(100,200)}px; height: ${randInt(100,200)}px; background: ${randColorHEX()}; margin-top: ${randInt(10,20)}px;`;
  updateStyle(); // 应用随机生成的样式
};

// 解析样式字符串为对象
const parseStyleString = (styleStr) => {
  const styles = {};
  const styleArray = styleStr.split(';');
  styleArray.forEach(style => {
    const [property, value] = style.split(':').map(s => s.trim());
    if (property && value) {
      styles[property] = value;
    }
  });
  return styles;
};
</script>

<style>
/* 可以根据需要添加样式 */
</style>
