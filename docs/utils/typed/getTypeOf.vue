<script setup lang="ts">
import { ref, computed } from "vue";
import { getTypeOf } from "buzzts";

const inputVal = ref<string>('123'); // 输入框字符串
const result = ref<string | null>(null);

// 预设示例集合，key是按钮名，value是对应的输入字符串
const examples: Record<string, string> = {
  '数字': '123',
  '字符串': '"hello world"',
  '布尔 true': 'true',
  '布尔 false': 'false',
  '空数组': '[]',
  '数字数组': '[1, 2, 3]',
  '空对象': '{}',
  '普通对象': '{"a":1,"b":2}',
  'null': 'null',
  'undefined': 'undefined',
  '函数表达式': 'function() {}',
  '箭头函数': '() => {}',
  'BigInt': 'BigInt("12345678901234567890")',
  'Symbol': 'Symbol("sym")',
  '日期对象': 'new Date("2023-01-01")',
  '正则表达式': '/^abc$/',
  '异步函数': 'async function() {}',
  '生成器函数': 'function*() {}',
  'Promise': 'Promise.resolve(123)',
  '类': 'class MyClass {}',
};

function setExample(key: string) {
  inputVal.value = examples[key];
  detectType();
}

function detectType() {
  let val: any;
  try {
    // 特殊处理部分示例字符串，eval安全性注意：这里只为演示，实际项目慎用eval
    if (inputVal.value === 'undefined') {
      val = undefined;
    } else if (
      inputVal.value.startsWith('function') ||
      inputVal.value.startsWith('() =>') ||
      inputVal.value.startsWith('async function') ||
      inputVal.value.startsWith('function*') ||
      inputVal.value.startsWith('class ') ||
      inputVal.value.startsWith('BigInt') ||
      inputVal.value.startsWith('Symbol') ||
      inputVal.value.startsWith('new Date') ||
      inputVal.value.startsWith('Promise') ||
      inputVal.value.startsWith('/')
    ) {
      // eslint-disable-next-line no-eval
      val = eval(`(${inputVal.value})`);
    } else {
      val = JSON.parse(inputVal.value);
    }
  } catch {
    val = inputVal.value;
  }
  result.value = getTypeOf(val);
}

const resultText = computed(() => {
  if (!result.value) return "请输入值并点击检测";
  return `getTypeOf(${inputVal.value}) = ${result.value}`;
});
</script>

<template>
  <n-card title="获取参数具体类型 - 多场景示例">
    <n-space vertical>
      <n-input
        v-model:value="inputVal"
        placeholder='输入值，例如 "123", "true", "[]" 或 "{}"'
        label="输入值"
        type="textarea"
        rows="3"
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

      <n-button type="primary" @click="detectType">检测</n-button>

      <n-gradient-text type="info" style="margin-top: 12px; display: block;">
        {{ resultText }}
      </n-gradient-text>
    </n-space>
  </n-card>
</template>
