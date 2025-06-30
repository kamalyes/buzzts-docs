<script setup lang="ts">
import { ref, computed, watch, onMounted } from "vue";
import { typeasy } from "buzzts";

type DemoItem = { label: string; value: unknown };

const demos: DemoItem[] = [
  { label: "数字 42", value: 42 },
  { label: "字符串", value: "hello" },
  { label: "布尔 true", value: true },
  { label: "null", value: null },
  { label: "undefined", value: undefined },
  { label: "NaN", value: NaN },
  { label: "Infinity", value: Infinity },
  { label: "-0", value: -0 },
  { label: "对象", value: {} },
  { label: "数组", value: [1, 2] },
  { label: "函数", value: () => {} },
  { label: "Symbol", value: Symbol("sym") },
  { label: "BigInt", value: BigInt(123) },
];

const selectedIndex = ref(0);
const val = ref(demos[0].value);
const result = ref<boolean | null>(null);

function checkIsPrimitive() {
  try {
    result.value = typeasy.isPrimitive(val.value);
  } catch {
    result.value = false;
  }
}

function selectDemo(index: number) {
  selectedIndex.value = index;
  val.value = demos[index].value;
  checkIsPrimitive();
}

watch(val, () => {
  checkIsPrimitive();
});

onMounted(() => {
  checkIsPrimitive();
});

const resultText = computed(() =>
  result.value === null
    ? "请选择或输入任意数据"
    : `typeasy.isPrimitive(${JSON.stringify(val.value)}) = ${result.value}`
);
</script>

<template>
  <n-card title="检测是否为原始类型 - typeasy.isPrimitive 多示例演示">
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

      <n-gradient-text v-if="result !== null" type="info" style="margin-top: 12px;">
        {{ resultText }}
      </n-gradient-text>
      <n-text v-else style="margin-top: 12px;">请选择或输入任意数据</n-text>
    </n-space>
  </n-card>
</template>
