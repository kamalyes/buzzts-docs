<script setup lang="ts">
import { ref, computed } from "vue";
import { capitalizeFirstLetter, randInt, randString, RandType } from "buzzts";

const input = ref<string>(randString(randInt(8, 18), RandType.LOWERCASE | RandType.NUMBER));
const result = ref<string>("");

function manualConvert() {
  // 直接转换当前输入框内容
  result.value = capitalizeFirstLetter(input.value);
}

function randomConvert() {
  // 先随机生成字符串赋值给输入框
  input.value = randString(randInt(8, 18), RandType.LOWERCASE | RandType.NUMBER);
  // 再转换
  result.value = capitalizeFirstLetter(input.value);
}

const resultText = computed(() => {
  if (!result.value) return "请输入字符串后点击转换";
  return `capitalizeFirstLetter() = ${result.value}`;
});
</script>

<template>
  <n-card title="首字母大写转换">
    <n-space vertical>
      <n-input v-model:value="input" label="输入字符串" />

      <n-space>
        <n-button type="info" @click="randomConvert">随机转换</n-button>
        <n-button type="primary" @click="manualConvert">手动转换</n-button>
      </n-space>

      <n-gradient-text type="info">{{ resultText }}</n-gradient-text>
    </n-space>
  </n-card>
</template>
