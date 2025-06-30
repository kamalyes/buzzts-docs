<script setup lang="ts">
import { ref, computed } from "vue";
import { mergeObject } from "buzzts";

type DemoItem = {
  label: string;
  source: object | undefined;
  defaults: object | undefined;
};

const demos: DemoItem[] = [
  {
    label: "覆盖默认值",
    source: { a: 1 },
    defaults: { a: 0, b: 2 },
  },
  {
    label: "深度合并",
    source: { a: { x: 1 }, b: 2 },
    defaults: { a: { y: 2 }, c: 3 },
  },
  {
    label: "含 null 值跳过",
    source: { a: null, b: 2 },
    defaults: { a: 1, b: 0 },
  },
  {
    label: "空对象合并",
    source: {},
    defaults: { a: 1 },
  },
  {
    label: "非对象参数",
    source: null,
    defaults: undefined,
  },
  {
    label: "合并数组",
    source: { arr: [1, 2] },
    defaults: { arr: [3, 4], other: 5 },
  },
  {
    label: "合并嵌套对象",
    source: { a: { x: 1 }, b: 2 },
    defaults: { a: { y: 2, z: 3 }, b: 3 },
  },
  {
    label: "覆盖数组",
    source: { arr: [1, 2] },
    defaults: { arr: [3, 4], other: 5 },
  },
  {
    label: "处理布尔值",
    source: { isActive: true },
    defaults: { isActive: false, isAdmin: false },
  },
];

const selectedIndex = ref(0);
const result = ref<object>({});

function runDemo(index: number) {
  selectedIndex.value = index;
  const demo = demos[index];
  result.value = mergeObject(demo.source, demo.defaults);
}

runDemo(selectedIndex.value);

const resultText = computed(() => {
  const demo = demos[selectedIndex.value];
  const source = demo.source === null ? 'null' : JSON.stringify(demo.source, null, 2);
  const defaults = demo.defaults === null ? 'null' : JSON.stringify(demo.defaults, null, 2);
  return `mergeObject(${source}, ${defaults}) = ${JSON.stringify(result.value, null, 2)}`;
});
</script>

<template>
  <n-card title="深拷贝合并对象 mergeObject - 多示例演示">
    <n-space vertical size="large">
      <n-space wrap>
        <n-button
          v-for="(item, index) in demos"
          :key="index"
          size="small"
          :type="selectedIndex === index ? 'primary' : 'default'"
          @click="runDemo(index)"
        >
          {{ item.label }}
        </n-button>
      </n-space>

      <n-gradient-text v-if="result !== null" type="info" style="margin-top: 12px;">
        {{ resultText }}
      </n-gradient-text>
    </n-space>
  </n-card>
</template>
