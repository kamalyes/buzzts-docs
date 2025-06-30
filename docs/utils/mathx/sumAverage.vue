<script setup lang="ts">
import { ref, computed } from "vue";
import { sumAverage, rangeWithStep } from "buzzts";

const demos = [
  [1, 2, 3, 4, 5],
  [10, 20, 30],
  [0, 0, 0],
  [-1, -2, -3],
  [100],
  rangeWithStep(1,40,2),
  rangeWithStep(-100,150,21)
];

const selectedIndex = ref(0);
const inputValue = ref(demos[0].join(","));
const result = ref<number | null>(null);

function runDemo(index: number) {
  selectedIndex.value = index;
  inputValue.value = demos[index].join(",");
  const arr = demos[index];
  result.value = sumAverage(arr);
}

function onInputChange() {
  const arr = inputValue.value
    .split(",")
    .map((v) => Number(v.trim()))
    .filter((v) => !isNaN(v));
  if (arr.length === 0) {
    result.value = null;
    return;
  }
  result.value = sumAverage(arr);
}

runDemo(selectedIndex.value);

const resultText = computed(() =>
  result.value === null
    ? "请选择或输入任意数据"
    : `sumAverage(${demos[selectedIndex.value]}) = ${result.value}`
);
</script>

<template>
  <n-card title="计算数组平均值 sumAverage - 多示例演示">
    <n-space vertical size="large">
      <n-space wrap>
        <n-button
          v-for="(item, index) in demos"
          :key="index"
          size="small"
          :type="selectedIndex === index ? 'primary' : 'default'"
          @click="runDemo(index)"
        >
          {{ item.join(",") }}
        </n-button>
      </n-space>

      <n-input v-model:value="inputValue" @input="onInputChange" placeholder="请输入数字数组，逗号分隔" />
      
      <n-gradient-text v-if="result !== null" type="info" style="margin-top: 12px;">
        {{ resultText }}
      </n-gradient-text>
    </n-space>
  </n-card>
</template>
