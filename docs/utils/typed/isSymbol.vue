<script setup lang="ts">
import { ref, computed } from "vue";
import { isSymbol } from "buzzts";

const inputStr = ref("Symbol('test')");
const result = ref<boolean | null>(null);

function parseInput(value: string): any {
  // 简单解析，如果是 Symbol('xxx') 格式，转换成 Symbol
  const symbolMatch = value.match(/^Symbol\((.*)\)$/);
  if (symbolMatch) {
    // 去掉两边的引号
    let desc = symbolMatch[1];
    if ((desc.startsWith("'") && desc.endsWith("'")) || (desc.startsWith('"') && desc.endsWith('"'))) {
      desc = desc.slice(1, -1);
    }
    return Symbol(desc);
  }
  // 你可以根据需要扩展更多类型转换
  return value;
}

function checkIsSymbol() {
  const val = parseInput(inputStr.value);
  result.value = isSymbol(val);
}

const resultText = computed(() => {
  if (result.value === null) return "请输入值并点击检测";
  return `isSymbol(${inputStr.value}) = ${result.value}`;
});
</script>

<template>
  <n-card title="判断是否为 Symbol 类型">
    <n-space vertical>
      <n-input v-model:value="inputStr" placeholder="输入任意值，例如 Symbol('test')" />
      <n-button type="primary" @click="checkIsSymbol">检测</n-button>
      <n-gradient-text type="info">{{ resultText }}</n-gradient-text>
    </n-space>
  </n-card>
</template>
