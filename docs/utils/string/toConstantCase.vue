<script setup lang="ts">
import { ref, computed } from "vue";
import { toConstantCase, randInt, randString, RandType } from "buzzts";

const input = ref<string>(randString(randInt(8, 18), RandType.LOWERCASE | RandType.CAPITAL | RandType.NUMBER));
const preserveNull = ref<boolean>(false);
const result = ref<string | null>("");

function generateConstant() {
  result.value = toConstantCase(input.value, { preserveNull: preserveNull.value });
}

// 新增随机转换函数
function randomConvert() {
  input.value = randString(randInt(8, 18), RandType.LOWERCASE | RandType.CAPITAL | RandType.NUMBER);
  generateConstant();
}

const resultText = computed(() => {
  if (result.value === null || result.value === '') return "请输入字符串后点击转换";
  return `toConstantCase() = ${result.value}`;
});
</script>

<template>
  <n-card title="转换为常量命名">
    <n-space vertical>
      <n-input v-model:value="input" label="输入字符串" />
      <n-checkbox-group v-model:value="preserveNull" multiple={false}>
        <n-checkbox :value="true">非字符串时保留原值</n-checkbox>
      </n-checkbox-group>

      <n-space>
        <n-button type="info" @click="randomConvert">随机转换</n-button>
        <n-button type="primary" @click="generateConstant">转换</n-button>
      </n-space>

      <n-gradient-text type="info">{{ resultText }}</n-gradient-text>
    </n-space>
  </n-card>
</template>
