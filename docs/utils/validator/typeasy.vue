<script setup lang="ts">
import { ref, computed, watch, onMounted } from "vue";
import typeasy from "buzzts";

type DemoItem = { label: string; value: unknown };

const demos: DemoItem[] = [
  { label: "null", value: null },
  { label: "undefined", value: undefined },
  { label: "数字 42", value: 42 },
  { label: "NaN", value: NaN },
  { label: "Infinity", value: Infinity },
  { label: "-0", value: -0 },
  { label: "数组", value: [1, 2, 3] },
  { label: "对象", value: { a: 1 } },
  { label: "正则", value: /abc/ },
  { label: "日期", value: new Date() },
  { label: "函数", value: () => {} },
  { label: "类", value: class {} },
  { label: "Map", value: new Map() },
  { label: "Set", value: new Set() },
  { label: "字符串", value: "hello" },
  { label: "布尔 true", value: true },
  { label: "Symbol", value: Symbol("sym") },
  { label: "BigInt", value: BigInt(123) },
];

const selectedIndex = ref(0);
const val = ref(demos[0].value);
const result = ref<string | null>(null);

function checkTypeasy() {
  try {
    result.value = typeasy(val.value);
  } catch {
    result.value = "error";
  }
}

function selectDemo(index: number) {
  selectedIndex.value = index;
  val.value = demos[index].value;
  checkTypeasy();
}

watch(val, () => {
  checkTypeasy();
});

onMounted(() => {
  checkTypeasy();
});

const resultText = computed(() =>
  result.value === null
    ? "请选择或输入任意数据"
    : `typeasy(${JSON.stringify(val.value)}) = "${result.value}"`
);
</script>

<template>
  <n-card title="基础数据类型检测 - typeasy 多示例演示">
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

      <!-- 这里用 textarea 展示 JSON 可以方便输入复杂数据 -->
      <n-input
        type="textarea"
        v-model:value="val"
        placeholder="请手动修改数据（JSON 格式）"
        @input="val = parseInput(val)"
        rows="3"
      />

      <n-gradient-text v-if="result !== null" type="info" style="margin-top: 12px;">
        {{ resultText }}
      </n-gradient-text>
      <n-text v-else style="margin-top: 12px;">请选择或输入任意数据</n-text>
    </n-space>
  </n-card>
</template>

<script lang="ts">
// 解析输入字符串为 JS 值，失败时保持字符串
function parseInput(input: string): unknown {
  try {
    return JSON.parse(input);
  } catch {
    return input;
  }
}
</script>
