<script setup lang="ts">
import { ref, computed, watch, onMounted } from "vue";
import { isArray } from "buzzts";

type DemoItem = { label: string; value: any };

const demos: DemoItem[] = [
  { label: "空数组", value: [] },
  { label: "数字数组", value: [1, 2, 3] },
  { label: "字符串数组", value: ["a", "b"] },
  { label: "对象", value: {} },
  { label: "字符串", value: "abc" },
  { label: "数字", value: 123 },
  { label: "null", value: null },
  { label: "undefined", value: undefined },
];

// 当前选中示例索引，-1表示无示例选中
const selectedIndex = ref(0);
const val = ref<any>(demos[0].value);
const result = ref<boolean | null>(null);

// 校验函数
function checkIsArray() {
  result.value = isArray(val.value);
}

// 点击示例按钮
function selectDemo(index: number) {
  selectedIndex.value = index;
  val.value = demos[index].value;
  checkIsArray(); // 选示例时自动校验
}

// 监听示例变化自动校验
watch(val, () => {
  checkIsArray();
});

// 页面加载时自动校验默认示例
onMounted(() => {
  checkIsArray();
});

const resultText = computed(() =>
  result.value === null
    ? "请选择示例"
    : `isArray(${typeof val.value}) = ${result.value}`
);
</script>

<template>
  <n-card title="判断是否为数组 - 多示例演示">
    <n-space vertical size="large">
      <n-space wrap>
        <!-- 多示例按钮 -->
        <n-button
          v-for="(item, index) in demos"
          :key="index"
          size="small"
          :type="selectedIndex === index ? 'primary' : 'default'"
          @click="selectDemo(index)"
        >
          {{ item.label }}
        </n-button>
      </n-space>

      <!-- 结果显示 -->
      <n-gradient-text v-if="result !== null" type="info" style="margin-top: 12px;">
        {{ resultText }}
      </n-gradient-text>
      <n-text v-else style="margin-top: 12px;">请选择示例</n-text>
    </n-space>
  </n-card>
</template>
