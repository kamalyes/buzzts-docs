<script setup lang="ts">
import { ref, computed } from "vue";
import { randTimestamp } from "buzzts";

const startTsStr = ref<string>("1672531200000"); // 例子时间戳
const endTsStr = ref<string>("1704067200000");
const tsResult = ref<number | null>(null);
const errorMsg = ref<string>("");

function generateRandTimestamp() {
  errorMsg.value = "";
  try {
    const startTs = Number(startTsStr.value);
    const endTs = Number(endTsStr.value);
    if (isNaN(startTs) || isNaN(endTs)) throw new Error("请输入有效数字时间戳");
    tsResult.value = randTimestamp(startTs, endTs);
  } catch (e: any) {
    errorMsg.value = e.message || "参数错误";
    tsResult.value = null;
  }
}

const tsText = computed(() => {
  if (errorMsg.value) return `错误: ${errorMsg.value}`;
  if (!tsResult.value) return "点击生成随机时间戳";
  return `randTimestamp() = ${tsResult.value} (${new Date(tsResult.value).toISOString()})`;
});
</script>

<template>
  <n-card title="随机时间戳生成">
    <n-space vertical>
      <n-input v-model:value="startTsStr" placeholder="起始时间戳（毫秒）" />
      <n-input v-model:value="endTsStr" placeholder="结束时间戳（毫秒）" />
      <n-button type="primary" @click="generateRandTimestamp">生成随机时间戳</n-button>

      <n-gradient-text type="info">{{ tsText }}</n-gradient-text>
    </n-space>
  </n-card>
</template>
