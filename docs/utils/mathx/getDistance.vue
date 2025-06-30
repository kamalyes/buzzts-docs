<script setup lang="ts">
import { ref, computed } from "vue";
import { getDistance } from "buzzts";

interface Point {
  x: number;
  y: number;
}

type DemoItem = {
  label: string;
  point1: Point;
  point2: Point;
};

const demos: DemoItem[] = [
  { label: "点(1,2) 到 点(3,4)", point1: { x: 1, y: 2 }, point2: { x: 3, y: 4 } },
  { label: "点(0,0) 到 点(0,0)", point1: { x: 0, y: 0 }, point2: { x: 0, y: 0 } },
  { label: "点(-1,-1) 到 点(1,1)", point1: { x: -1, y: -1 }, point2: { x: 1, y: 1 } },
];

const selectedIndex = ref(0);
const distance = ref<number>(0);

function runDemo(index: number) {
  selectedIndex.value = index;
  const demo = demos[index];
  distance.value = getDistance(demo.point1, demo.point2);
}

runDemo(selectedIndex.value);
</script>

<template>
  <n-card title="计算两坐标点之间的距离 getDistance - 多示例演示">
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

      <n-text style="margin-top: 12px;">距离：{{ distance }}</n-text>
    </n-space>
  </n-card>
</template>
