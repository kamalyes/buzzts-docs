<script setup lang="ts">
import { ref, onMounted } from "vue";
import { isEmpty } from "buzzts";

// 多个示例值，涵盖常见空值和非空值
const demos = [
  { label: "null", value: String(null) },             // "null"
  { label: "undefined", value: String(undefined) },   // "undefined"
  { label: "空字符串", value: "" },
  { label: "空数组", value: JSON.stringify([]) },     // "[]"
  { label: "空对象", value: JSON.stringify({}) },     // "{}"
  { label: "数字 0", value: String(0) },              // "0"
  { label: "字符串 '0'", value: "0" },
  { label: "布尔 false", value: String(false) },      // "false"
  { label: "非空字符串", value: "hello" },
  { label: "非空数组", value: JSON.stringify([1, 2]) }, // "[1,2]"
  { label: "非空对象", value: JSON.stringify({ a: 1 }) }, // '{"a":1}'
  { label: "空格", value: "   " },
  { label: "制表符", value: "\t\t" },
  { label: "换行符", value: "\n" },
  { label: "空白混合", value: " \t\n " },
  { label: "数字字符串", value: "123" },
];

// 结果数组
const results = ref<
  {
    label: string;
    value: any;
    isEmpty: boolean;
  }[]
>([]);

onMounted(() => {
  results.value = demos.map((demo) => ({
    label: demo.label,
    value: demo.value,
    isEmpty: isEmpty(demo.value),
  }));
});
</script>

<template>
  <n-card title="判断是否为空值 - 示例演示">
    <n-space vertical>
      <div v-for="(item, index) in results" :key="index" style="padding: 6px 0;">
        <strong>{{ item.label }}：</strong>
        <span>值：
          <code>
            {{
              item.value === null
                ? "null"
                : item.value === undefined
                ? "undefined"
                : JSON.stringify(item.value)
            }}
          </code>
        </span>
        <span style="margin-left: 12px;">
          结果：
          <span :style="{ color: item.isEmpty ? 'green' : 'red' }">
            {{ item.isEmpty }}
          </span>
        </span>
      </div>
    </n-space>
  </n-card>
</template>
