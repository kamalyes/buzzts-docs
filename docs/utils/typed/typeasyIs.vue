<script setup lang="ts">
import { ref, computed, watch, onMounted } from "vue";
import { typeasy } from "buzzts";

type DemoItem = { label: string; value: unknown; typeStr: string };

const demos: DemoItem[] = [
  { label: "数组", value: [1, 2, 3], typeStr: "array" },
  { label: "日期", value: new Date(), typeStr: "date" },
  { label: "字符串", value: "hello", typeStr: "string" },
  { label: "数字", value: 123, typeStr: "number" },
  { label: "函数", value: () => {}, typeStr: "function" },
  { label: "正则", value: /abc/, typeStr: "regexp" },
  { label: "空对象", value: {}, typeStr: "object" },
  { label: "Map", value: new Map(), typeStr: "map" },
  { label: "Set", value: new Set(), typeStr: "set" },
  { label: "null", value: null, typeStr: "null" },
  { label: "undefined", value: undefined, typeStr: "undefined" },
];

const selectedIndex = ref(0);
const val = ref(demos[0].value);
const typeStr = ref(demos[0].typeStr);
const result = ref<boolean | null>(null);

function checkTypeIs() {
  try {
    result.value = typeasy.is(val.value, typeStr.value);
  } catch {
    result.value = false;
  }
}

function selectDemo(index: number) {
  selectedIndex.value = index;
  val.value = demos[index].value;
  typeStr.value = demos[index].typeStr;
  checkTypeIs();
}

watch([val, typeStr], () => {
  checkTypeIs();
});

onMounted(() => {
  checkTypeIs();
});

const resultText = computed(() =>
  result.value === null
    ? "请选择示例或输入值和类型"
    : `typeasy.is(${JSON.stringify(val.value)}, "${typeStr.value}") = ${result.value}`
);
</script>

<template>
  <n-card title="精确类型验证 - typeasy.is 多示例演示">
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

      <n-input
        v-model:value="typeStr"
        placeholder="请输入预期类型字符串"
      />

      <n-gradient-text v-if="result !== null" type="info" style="margin-top: 12px;">
        {{ resultText }}
      </n-gradient-text>
      <n-text v-else style="margin-top: 12px;">请选择示例或输入值和类型</n-text>
    </n-space>
  </n-card>
</template>
