<script setup lang="ts">
import { ref } from "vue";
import { TimeoutPromise, randInt } from "buzzts";

// 无超时随机延迟相关
const delayRunning = ref(false);
const delayResult = ref("");
const delayTime = ref(0);

async function runDelayOnly() {
  delayRunning.value = true;
  delayResult.value = "等待中...";
  delayTime.value = randInt(500, 4000);

  const p = new Promise<string>((resolve) => {
    setTimeout(() => resolve(`延迟 ${delayTime.value} ms 完成`), delayTime.value);
  });

  try {
    const res = await p;
    delayResult.value = `成功: ${res}`;
  } catch (e: any) {
    delayResult.value = `失败: ${e.message}`;
  } finally {
    delayRunning.value = false;
  }
}

// 随机延迟 + 超时相关
const timeoutRunning = ref(false);
const timeoutResult = ref("");
const timeoutDelay = ref(0);
const timeoutLimit = ref(0);

async function runDelayWithTimeout() {
  timeoutRunning.value = true;
  timeoutResult.value = "等待中...";
  timeoutDelay.value = randInt(500, 1500);
  timeoutLimit.value = randInt(timeoutDelay.value + 500, 3000);

  const p = new Promise<string>((resolve) => {
    setTimeout(() => resolve(`延迟 ${timeoutDelay.value} ms 完成`), timeoutDelay.value);
  });

  const tp = new TimeoutPromise(p, timeoutLimit.value);

  try {
    const res = await tp.promise;
    timeoutResult.value = `成功: ${res} （超时设置：${timeoutLimit.value} ms）`;
  } catch (e: any) {
    timeoutResult.value = `失败: ${e.message} （延迟 ${timeoutDelay.value} ms，超时 ${timeoutLimit.value} ms）`;
  } finally {
    timeoutRunning.value = false;
  }
}
</script>

<template>
  <n-card title="随机延迟与超时演示，两个按钮独立控制">
    <n-space vertical size="large">
      <!-- 无超时随机延迟 -->
      <n-card title="无超时随机延迟" size="small">
        <n-button
          type="primary"
          :loading="delayRunning"
          @click="runDelayOnly"
        >
          运行随机延迟（无超时）
        </n-button>
        <n-text style="display: block; margin-top: 8px;">{{ delayResult }}</n-text>
      </n-card>

      <!-- 随机延迟 + 超时 -->
      <n-card title="随机延迟 + 超时" size="small">
        <n-button
          type="warning"
          :loading="timeoutRunning"
          @click="runDelayWithTimeout"
        >
          运行随机延迟 + 超时
        </n-button>
        <n-text style="display: block; margin-top: 8px;">{{ timeoutResult }}</n-text>
      </n-card>
    </n-space>
  </n-card>
</template>
