<script setup lang="ts">
import { ref, reactive, computed } from "vue";
import { truncateText, RandType, randInt, randString } from "buzzts";

interface Example {
  text: string;
  maxLength: number;
}

const examples: Example[] = [
  { text: "Hello world", maxLength: 7 },
  { text: "Hello world", maxLength: 10 },
  { text: "你好，世界！", maxLength: 10 },
  { text: "🙂🙃🙂🙃", maxLength: 2 },
  { text: "🙂🙃🙂🙃", maxLength: 1 },
  { text: "Hello", maxLength: 3 },
];

// 计算示例的截断结果
const exampleResults = computed(() =>
  examples.map((ex) =>
    truncateText(ex.text, ex.maxLength, { ellipsis: "..." })
  )
);
</script>

<template>
  <n-card title="多组智能截断字符串">
    <n-divider>示例展示</n-divider>
    <n-space vertical>
      <div
        v-for="(ex, i) in examples"
        :key="i"
        style="border: 1px solid #eee; padding: 8px; border-radius: 4px; margin-top: 8px;"
      >
        <div><strong>原文：</strong>{{ ex.text }}</div>
        <div><strong>最大长度：</strong>{{ ex.maxLength }}</div>
        <div><strong>截断结果：</strong>{{ exampleResults[i] }}</div>
      </div>
    </n-space>
  </n-card>
</template>
