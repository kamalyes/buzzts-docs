<script setup lang="ts">
import { ref, computed } from "vue";
import { isFunction } from "buzzts";

type DemoItem = { label: string; value: unknown };

const demos: DemoItem[] = [
  { label: "普通函数", value: function foo() {} },
  { label: "箭头函数", value: () => {} },
  { label: "类方法", value: class A { method() {} }.prototype.method },
  { label: "字符串", value: "function" },
  { label: "数字", value: 123 },
  { label: "null", value: null },
  { label: "对象", value: { a: 1 } },
];

const selectedIndex = ref(0);
const val = ref<unknown>(demos[0].value);
const result = ref<boolean | null>(null);

function checkIsFunction() {
  result.value = isFunction(val.value);
}

function selectDemo(index: number) {
  selectedIndex.value = index;
  val.value = demos[index].value;
  result.value = null;
}

const formatValue = (v: unknown): string => {
  if (typeof v === "function") return v.toString();
  try {
    return JSON.stringify(v);
  } catch {
    return String(v);
  }
};

const resultText = computed(() =>
  result.value === null
    ? "请选择示例后点击检测是否为函数"
    : `isFunction(${formatValue(val.value)}) = ${result.value}`
);
</script>

<template>
  <n-card title="判断是否为函数 - 多示例演示">
    <n-space vertical size="large">
      <n-select
        v-model:value="selectedIndex"
        :options="demos.map((d, i) => ({ label: d.label, value: i }))"
        @update:value="selectDemo"
        style="width: 220px"
        clearable
      />
      <n-input
        :value="formatValue(val)"
        placeholder="当前示例值"
        readonly
      />
      <n-button type="primary" @click="checkIsFunction">检测</n-button>
      <n-gradient-text v-if="result !== null" type="info">{{ resultText }}</n-gradient-text>
      <n-text v-else>请选择示例并点击检测</n-text>
    </n-space>
  </n-card>
</template>
