<script setup lang="ts">
import { ref, computed } from "vue";
import { intToLowerChinese, randInt } from "buzzts";

const demos = [
  0,
  10,
  123456789,
  10001,
  "100000000",
  "abc", // 非法输入示例
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
const result = ref<string | null>(null);
const errorMsg = ref<string>("");

function runDemo(index: number) {
  selectedIndex.value = index;
  inputValue.value = String(demos[index]);
  try {
    result.value = intToLowerChinese(inputValue.value);
    errorMsg.value = "";
  } catch (e: any) {
    result.value = null;
    errorMsg.value = e.message || "输入错误";
  }
}

function onInputChange() {
  try {
    result.value = intToLowerChinese(inputValue.value);
    errorMsg.value = "";
  } catch (e: any) {
    result.value = null;
    errorMsg.value = e.message || "输入错误";
  }
}

runDemo(selectedIndex.value);
</script>

<template>
  <n-card title="数字转中文(小写) intToLowerChinese - 多示例演示">
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

      <n-input v-model:value="inputValue" @input="onInputChange" placeholder="请输入非负整数" />

      <n-text v-if="result !== null" style="margin-top: 12px;">转换结果：{{ result }}</n-text>
      <n-text v-else type="error" style="margin-top: 12px;">{{ errorMsg }}</n-text>
    </n-space>
  </n-card>
</template>
