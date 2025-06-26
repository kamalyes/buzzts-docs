<script setup lang="ts">
import { ref, computed } from "vue";
import { snakeToCamel, randInt, randString, RandType } from "buzzts";

const input = ref<string>(randString(randInt(8, 18), RandType.LOWERCASE | RandType.CAPITAL | RandType.NUMBER));
const pascalCase = ref<boolean>(false);
const result = ref<string>("");

function generateCamel() {
  result.value = snakeToCamel(input.value, { pascalCase: pascalCase.value });
}

// 新增随机转换函数
function randomConvert() {
  input.value = randString(randInt(8, 18), RandType.LOWERCASE | RandType.CAPITAL | RandType.NUMBER);
  generateCamel();
}

const resultText = computed(() => {
  if (!result.value) return "请输入蛇形命名字符串后点击转换";
  return `snakeToCamel() = ${result.value}`;
});
</script>

<template>
  <n-card title="蛇形转驼峰命名">
    <n-space vertical>
      <n-input v-model:value="input" label="蛇形命名字符串" />
      <n-checkbox-group v-model:value="pascalCase" multiple={false}>
        <n-checkbox :value="true">转换为帕斯卡命名</n-checkbox>
      </n-checkbox-group>

      <n-space>
        <n-button type="info" @click="randomConvert">随机转换</n-button>
        <n-button type="primary" @click="generateCamel">转换</n-button>
      </n-space>

      <n-gradient-text type="info">{{ resultText }}</n-gradient-text>
    </n-space>
  </n-card>
</template>
