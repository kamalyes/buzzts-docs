<script setup lang="ts">
import { ref, computed, watch, onMounted } from "vue";
import { getBetween } from "buzzts";

type DemoItem = {
  label: string;
  start: any;
  end: any;
  step?: number;
  compare?: (current: any, end: any) => boolean;
  next: (current: any, step: number) => any;
};

function nextDate(current: Date, step: number): Date {
  const d = new Date(current);
  d.setDate(d.getDate() + step);
  return d;
}

function nextChar(c: string, step: number): string {
  return String.fromCharCode(c.charCodeAt(0) + step);
}

const demos: DemoItem[] = [
  {
    label: "数字区间 1 到 5",
    start: 1,
    end: 5,
    step: 1,
    next: (current, step) => current + step,
  },
  {
    label: "日期区间 2023-06-20 到 2023-06-23",
    start: new Date("2023-06-20T00:00:00"),
    end: new Date("2023-06-23T00:00:00"),
    step: 1,
    compare: (current, end) => current <= end,
    next: nextDate,
  },
  {
    label: "字符区间 'a' 到 'e'",
    start: "a",
    end: "e",
    step: 1,
    compare: (current, end) => current.charCodeAt(0) <= end.charCodeAt(0),
    next: nextChar,
  },
  {
    label: "无效输入（start=null）",
    start: null,
    end: 5,
    step: 1,
    next: (current, step) => current + step,
  },
];

const selectedIndex = ref(0);
const result = ref<any[] | null>(null);
const funcName = ref<string | null>(null);
const funcParams = ref<string | null>(null);

function runDemo(index: number) {
  selectedIndex.value = index;
  const demo = demos[index];
  funcName.value = demo.next.name; // 获取调用的函数名
  funcParams.value = `${demo.start},${demo.end},${demo.step}`; // 参数字符串

  try {
    result.value = getBetween(demo.start, demo.end, {
      step: demo.step,
      compare: demo.compare,
      next: demo.next,
    });
  } catch (e) {
    result.value = null;
  }
}

watch(selectedIndex, (newIndex) => {
  runDemo(newIndex);
});

onMounted(() => {
  runDemo(selectedIndex.value);
});

const resultText = computed(() => {
  return  `getBetween(${funcParams.value})= ${JSON.stringify(result.value)}\n`;
});

</script>

<template>
  <n-card title="通用区间遍历函数 getBetween - 多示例演示">
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
