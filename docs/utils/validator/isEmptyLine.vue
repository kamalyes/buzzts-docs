<script setup lang="ts">
import { ref, computed, watch, onMounted } from "vue";
import { isEmptyLine } from "buzzts";

type DemoItem = { label: string; value: string };

const demos: DemoItem[] = [
  { label: "null", value: String(null) },             // "null"
  { label: "undefined", value: String(undefined) },   // "undefined"
  { label: "空字符串", value: "" },
  { label: "空数组", value: JSON.stringify([]) },     // "[]"
  { label: "空对象", value: JSON.stringify({}) },     // "{}"
  { label: "数字 0", value: String(0) },              // "0"
  { label: "字符串 '0'", value: "0" },
  { label: "布尔 false", value: String(false) },      // "false"
  { label: "非空字符串", value: "hello" },
  { label: "非空数组", value: JSON.stringify([1, 2]) }, // "[1,2]"
  { label: "非空对象", value: JSON.stringify({ a: 1 }) }, // '{"a":1}'
  { label: "空格", value: "   " },
  { label: "制表符", value: "\t\t" },
  { label: "换行符", value: "\n" },
  { label: "空白混合", value: " \t\n " },
  { label: "数字字符串", value: "123" },
];

const selectedIndex = ref(0);
const val = ref(demos[0].value);
const result = ref<boolean | null>(null);

function checkEmptyLine() {
  result.value = isEmptyLine(val.value);
}

function selectDemo(index: number) {
  selectedIndex.value = index;
  val.value = demos[index].value;
  checkEmptyLine();
}

watch(val, () => {
  checkEmptyLine();
});

onMounted(() => {
  checkEmptyLine();
});

const resultText = computed(() =>
  result.value === null
    ? "请输入字符串或选择示例"
    : `isEmptyLine(${JSON.stringify(val.value)}) = ${result.value}`
);
</script>

<template>
  <n-card title="是否为空行校验（仅空白字符） - 多示例演示">
    <n-space vertical size="large">
      <n-space wrap>
        <n-button
          v-for="(item, index) in demos"
          :key="index"
          size="small"
          :type="selectedIndex === index ? 'primary' : 'default'"
          @click="selectDemo(index)"
        >
          {{ item.label }}
        </n-button>
      </n-space>

      <n-input v-model:value="val" placeholder="请输入自定义字符串" />

      <n-button type="primary" @click="checkEmptyLine">校验</n-button>

      <n-gradient-text v-if="result !== null" type="info" style="margin-top: 12px;">
        {{ resultText }}
      </n-gradient-text>
      <n-text v-else style="margin-top: 12px;">请输入字符串或选择示例</n-text>
    </n-space>
  </n-card>
</template>
