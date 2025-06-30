<script setup lang="ts">
import { ref, onMounted } from "vue";
import { isIPv4 } from "buzzts";

// 多示例，包含合法和非法IPv4地址
const demos = [
  { label: "合法 - 标准地址", value: "192.168.1.1" },
  { label: "合法 - 边界值0", value: "0.0.0.0" },
  { label: "合法 - 边界值255", value: "255.255.255.255" },
  { label: "非法 - 段数不足", value: "192.168.1" },
  { label: "非法 - 段数过多", value: "192.168.1.1.1" },
  { label: "非法 - 非数字字符", value: "192.168.one.1" },
  { label: "非法 - 前导零", value: "192.168.01.1" },
  { label: "非法 - 数字超范围", value: "256.100.100.100" },
  { label: "空字符串", value: "" },
  { label: "undefined", value: undefined },
  { label: "null", value: null },
  { label: "数字类型", value: 12345 },
];

// 保存所有示例的检测结果
const results = ref<
  {
    label: string;
    value: string | undefined | null | number;
    isValid: boolean;
  }[]
>([]);

function checkIsIPv4(value: unknown): boolean {
  // 先转字符串再判断，防止非字符串类型报错
  return isIPv4(value + "");
}

onMounted(() => {
  // 页面加载时自动检测所有示例
  results.value = demos.map((demo) => ({
    label: demo.label,
    value: demo.value,
    isValid: checkIsIPv4(demo.value),
  }));
});
</script>

<template>
  <n-card title="判断是否为合法IPv4地址 - 自动展示所有示例检测结果">
    <n-space vertical>
      <div v-for="(item, index) in results" :key="index" style="padding: 6px 0;">
        <strong>{{ item.label }}：</strong>
        <span>输入值：<code>{{ item.value === undefined ? "undefined" : item.value === null ? "null" : item.value }}</code></span>
        <span style="margin-left: 12px;">
          结果：
          <span :style="{ color: item.isValid ? 'green' : 'red' }">
            {{ item.isValid }}
          </span>
        </span>
      </div>
    </n-space>
  </n-card>
</template>
