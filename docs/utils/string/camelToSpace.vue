<script setup lang="ts">
import { ref, computed } from "vue";
import { camelToSpace, randInt, randString, RandType } from "buzzts";

const input = ref<string>(randString(randInt(8, 18), RandType.LOWERCASE | RandType.CAPITAL | RandType.NUMBER));
const capitalize = ref<boolean>(false);
const result = ref<string>("");

function generateSpace() {
  result.value = camelToSpace(input.value, { capitalize: capitalize.value });
}

// 新增随机转换函数
function randomConvert() {
  input.value = randString(randInt(8, 18), RandType.LOWERCASE | RandType.CAPITAL | RandType.NUMBER);
  generateSpace();
}

const resultText = computed(() => {
  if (!result.value) return "请输入驼峰命名字符串后点击转换";
  return `camelToSpace() = ${result.value}`;
});
</script>

<template>
  <n-card title="驼峰转空格命名">
    <n-space vertical>
      <n-input v-model:value="input" label="驼峰命名字符串" />

      <n-checkbox-group v-model:value="capitalize" multiple={false}>
        <n-checkbox :value="true">首字母大写</n-checkbox>
      </n-checkbox-group>

      <n-space>
        <n-button type="info" @click="randomConvert">随机转换</n-button>
        <n-button type="primary" @click="generateSpace">转换</n-button>
      </n-space>

      <n-gradient-text type="info">{{ resultText }}</n-gradient-text>
    </n-space>
  </n-card>
</template>
