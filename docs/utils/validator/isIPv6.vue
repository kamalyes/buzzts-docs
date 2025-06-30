<script setup lang="ts">
import { ref, onMounted } from "vue";
import { isIPv6 } from "buzzts";

const demos = [
  { label: "合法 - 标准完整地址", value: "2001:0db8:85a3:0000:0000:8a2e:0370:7334" },
  { label: "合法 - 压缩格式", value: "2001:0db8:85a3::8a2e:0370:7334" },
  { label: "合法 - 全零压缩", value: "::" },
  { label: "非法 - 包含IPv4格式", value: "2001:db8::192.168.1.1" },
  { label: "非法 - 冒号过多", value: "2001:::85a3::8a2e:0370:7334" },
  { label: "非法 - 非法字符", value: "2001:0db8:85a3::8a2e:0370:zzzz" },
  { label: "空字符串", value: "" },
  { label: "undefined", value: undefined },
  { label: "null", value: null },
  { label: "数字类型", value: 12345 },
];

const results = ref<
  {
    label: string;
    value: string | undefined | null | number;
    isValid: boolean;
  }[]
>([]);

function checkIsIPv6(value: unknown): boolean {
  if (typeof value !== "string") {
    if (value === undefined || value === null) return false;
    value = String(value);
  }
  // 如果不允许IPv4嵌套，可以加个简单判断
  if ((value as string).includes(".")) return false;

  return isIPv6(value as string);
}

onMounted(() => {
  results.value = demos.map((demo) => ({
    label: demo.label,
    value: demo.value,
    isValid: checkIsIPv6(demo.value),
  }));
});
</script>

<template>
  <n-card title="判断是否为合法IPv6地址 - 自动展示示例检测结果">
    <n-space vertical>
      <div
        v-for="(item, index) in results"
        :key="index"
        style="padding: 6px 0; border-bottom: 1px solid #eee;"
      >
        <strong>{{ item.label }}：</strong>
        <span>输入值：
          <code
            >{{ item.value === undefined
              ? "undefined"
              : item.value === null
              ? "null"
              : item.value }}</code
          >
        </span>
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
