<script setup lang="ts">
import { ref, computed } from "vue";
import { camelToSnake, randInt, randString, RandType } from "buzzts";

const input = ref<string>(randString(randInt(8, 18), RandType.LOWERCASE | RandType.CAPITAL | RandType.NUMBER));
const keepUnderscorePrefix = ref<boolean>(false);
const result = ref<string>("");

function generateSnake() {
  result.value = camelToSnake(input.value, { keepUnderscorePrefix: keepUnderscorePrefix.value });
}

// 新增随机转换函数
function randomConvert() {
  input.value = randString(randInt(8, 18), RandType.LOWERCASE | RandType.CAPITAL | RandType.NUMBER);
  generateSnake();
}

const resultText = computed(() => {
  if (!result.value) return "请输入驼峰命名字符串后点击转换";
  return `camelToSnake() = ${result.value}`;
});
</script>

<template>
  <n-card title="驼峰转蛇形命名">
    <n-space vertical>
      <n-input v-model:value="input" label="驼峰命名字符串" />

      <n-checkbox-group v-model:value="keepUnderscorePrefix" multiple={false}>
        <n-checkbox :value="true">保留前导下划线</n-checkbox>
      </n-checkbox-group>

      <n-space>
        <n-button type="info" @click="randomConvert">随机转换</n-button>
        <n-button type="primary" @click="generateSnake">转换</n-button>
      </n-space>

      <n-gradient-text type="info">{{ resultText }}</n-gradient-text>
    </n-space>
  </n-card>
</template>
