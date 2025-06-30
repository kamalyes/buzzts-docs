<script setup lang="ts">
import { ref, onMounted } from "vue";
import { isNil } from "buzzts";

// 示例值集合，包含 null、undefined 和其他各种类型
const demos = [
  { label: "null", value: null },
  { label: "undefined", value: undefined },
  { label: "空字符串", value: "" },
  { label: "数字 0", value: 0 },
  { label: "字符串 'null'", value: "null" },
  { label: "字符串 'undefined'", value: "undefined" },
  { label: "布尔 false", value: false },
  { label: "空数组", value: [] },
  { label: "空对象", value: {} },
];

// 用于存储检测结果
const results = ref<
  {
    label: string;
    value: any;
    isNil: boolean;
  }[]
>([]);

onMounted(() => {
  results.value = demos.map((demo) => ({
    label: demo.label,
    value: demo.value,
    isNil: isNil(demo.value),
  }));
});
</script>

<template>
  <n-card title="判断是否为 null 或 undefined - 自动展示示例检测结果">
    <n-space vertical>
      <div v-for="(item, index) in results" :key="index" style="padding: 6px 0;">
        <strong>{{ item.label }}：</strong>
        <span>值：<code>{{ item.value === undefined ? "undefined" : JSON.stringify(item.value) }}</code></span>
        <span style="margin-left: 12px;">
          结果：
          <span :style="{ color: item.isNil ? 'green' : 'red' }">
            {{ item.isNil }}
          </span>
        </span>
      </div>
    </n-space>
  </n-card>
</template>
