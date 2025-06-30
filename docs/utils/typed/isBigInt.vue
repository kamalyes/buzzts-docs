<script setup lang="ts">
import { ref, computed } from "vue";
import { isBigInt } from "buzzts";

const inputVal = ref<string>("123"); // 默认字符串输入
const result = ref<boolean | null>(null);

const examples: Record<string, string> = {
  '普通数字字符串': '123',
  '超大数字字符串': '1234567890123456789012345678901234567890',
  'BigInt 构造': 'BigInt("1234567890123456789012345678901234567890")',
  '负数字字符串': '-12345678901234567890',
  '0': '0',
  '负零字符串': '-0',
  '空字符串': '""',
  '非数字字符串': '"abc123"',
  '科学计数法字符串': '1e10',
  '带空格数字': '  9876543210  ',
  '带加号数字': '+123456',
  'BigInt 负数构造': 'BigInt("-98765432109876543210")',
  '字符串 true': '"true"',
  '布尔 true': 'true',
  'null': 'null',
  'undefined': 'undefined',
};

function setExample(key: string) {
  inputVal.value = examples[key];
  checkIsBigInt();
}

function checkIsBigInt() {
  try {
    let val: any;
    const str = inputVal.value.trim();

    if (str.startsWith('BigInt')) {
      // eslint-disable-next-line no-eval
      val = eval(str);
    } else if (str === 'undefined') {
      val = undefined;
    } else if (str === 'null') {
      val = null;
    } else if (str === 'true') {
      val = true;
    } else if (str === 'false') {
      val = false;
    } else {
      // 直接转 BigInt，非数字字符串会抛异常
      val = BigInt(str);
    }
    result.value = isBigInt(val);
  } catch {
    result.value = false;
  }
}

const resultText = computed(() => {
  if (result.value === null) return "请输入值并点击检测";
  return `isBigInt(${inputVal.value.trim()}) = ${result.value}`;
});
</script>

<template>
  <n-card title="判断是否为 BigInt 类型 - 多场景示例">
    <n-space vertical>
      <n-input
        v-model:value="inputVal"
        placeholder="输入数字字符串或 BigInt 表达式"
        label="输入值"
      />

      <n-space wrap>
        <n-button
          v-for="(val, key) in examples"
          :key="key"
          size="small"
          @click="setExample(key)"
        >
          {{ key }}
        </n-button>
      </n-space>

      <n-button type="primary" @click="checkIsBigInt">检测</n-button>

      <n-gradient-text
        type="info"
        style="margin-top: 12px; display: block;"
      >
        {{ resultText }}
      </n-gradient-text>
    </n-space>
  </n-card>
</template>
