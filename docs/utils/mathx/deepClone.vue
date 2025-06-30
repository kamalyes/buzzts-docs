<script setup lang="ts">
import { ref, computed } from "vue";
import { deepClone } from "buzzts";

type DemoItem = {
  label: string;
  obj: any;
};

const demos: DemoItem[] = [
  {
    label: "简单对象",
    obj: { a: 1, b: 2 },
  },
  {
    label: "嵌套对象",
    obj: { a: { x: 1 }, b: [1, 2, 3] },
  },
  {
    label: "日期和正则",
    obj: { date: new Date("2023-06-01"), reg: /test/i },
  },
];

const selectedIndex = ref(0);
const cloned = ref<any>(null);

function runDemo(index: number) {
  selectedIndex.value = index;
  const demo = demos[index];
  cloned.value = deepClone(demo.obj);
}

runDemo(selectedIndex.value);

function safeStringify(obj: any): string {
  try {
    return JSON.stringify(obj, null, 2);
  } catch {
    return String(obj);
  }
}

const resultText = computed(() => {
  const demo = demos[selectedIndex.value];
  const objStr = demo.obj === null ? 'null' : safeStringify(demo.obj);
  const clonedStr = safeStringify(cloned.value);
  return `deepClone(${objStr}) = ${clonedStr}`;
});

</script>

<template>
  <n-card title="深度复制对象 deepClone - 多示例演示">
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
