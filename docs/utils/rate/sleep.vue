<script setup lang="ts">
import { ref } from "vue";
import { Sleep, randInt } from "buzzts";

const sleepRunning = ref(false);
const sleepResult = ref<string>("");
const wait = ref(0);

let sleepInstance: Sleep | null = null;

async function runSleepDemo() {
  sleepRunning.value = true;
  sleepResult.value = "等待中...";
  wait.value = randInt(500, 2000); // 更新 ref
  sleepInstance = new Sleep(wait.value, () => {
    sleepResult.value = `Sleep 回调: 等待 ${wait.value} ms 完成`;
  });
  try {
    await sleepInstance.promise;
    sleepResult.value = `Sleep Promise resolved after ${wait.value} ms`;
  } catch (e: any) {
    sleepResult.value = `${e.message}`;
  } finally {
    sleepRunning.value = false;
    sleepInstance = null;
  }
}

function cancelSleep() {
  if (sleepInstance) {
    sleepInstance.cancel();
    sleepResult.value = "Sleep 已取消";
    sleepRunning.value = false;
    sleepInstance = null;
  }
}
</script>

<template>
  <n-card title="Sleep 类演示（随机等待时间，可取消）">
    <n-space vertical size="large">
      <n-space>
        <n-button
          type="primary"
          :loading="sleepRunning"
          @click="runSleepDemo"
        >
          运行 Sleep（随机等待 {{ wait }} ms）
        </n-button>
        <n-button
          type="error"
          :disabled="!sleepRunning"
          @click="cancelSleep"
        >
          取消 Sleep
        </n-button>
      </n-space>

      <n-text style="display: block; margin-top: 8px;">{{ sleepResult }}</n-text>
    </n-space>
  </n-card>
</template>
