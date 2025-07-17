<script setup lang="ts">
import { ref, computed } from "vue";
import { upperMoney, randInt } from "buzzts";

const demos = [
  123456789.123,
  0,
  -9876.54,
  NaN,
  100000000,
];

let randomMin = 500000000;
let randomMax = 1000000000;  // 初始max比min大

for (let i = 1; i <= 5; i++) {  // i从1开始，避免乘0
  demos.push(randInt(randomMin, randomMax));

  // 更新区间，让下一轮区间扩大
  randomMin = randomMax + 1;  
  randomMax = randomMax * 2;  // 让max指数级增长，比如翻倍
}

const selectedIndex = ref(0);
const inputValue = ref(String(demos[0]));
const result = ref("");

function runDemo(index: number) {
  selectedIndex.value = index;
  inputValue.value = String(demos[index]);
  result.value = upperMoney(Number(inputValue.value));
}

function onInputChange() {
  const num = Number(inputValue.value);
  result.value = upperMoney(num);
}

runDemo(selectedIndex.value);
</script>

<template>
  <n-card title="现金额转大写 upperMoney - 多示例演示">
    <n-space vertical size="large">
      <n-space wrap>
        <n-button
          v-for="(item, index) in demos"
          :key="index"
          size="small"
          :type="selectedIndex === index ? 'primary' : 'default'"
          @click="runDemo(index)"
        >
          {{ item }}
        </n-button>
      </n-space>

      <n-input v-model:value="inputValue" @input="onInputChange" placeholder="请输入数字" />

      <n-text style="margin-top: 12px;">转换结果：{{ result }}</n-text>
    </n-space>
  </n-card>
</template>
