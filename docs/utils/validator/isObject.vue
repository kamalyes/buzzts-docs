<script setup lang="ts">
import { ref, computed, watch, onMounted } from "vue";
import { isObject } from "buzzts";

type DemoItem = { label: string; value: any };

const demos: DemoItem[] = [
  { label: "空对象", value: {} },
  { label: "带属性对象", value: { a: 1 } },
  { label: "数组", value: [1, 2] },
  { label: "null", value: null },
  { label: "函数", value: () => {} },
  { label: "数字", value: 123 },
  { label: "字符串", value: "abc" },
];

// 当前选中示例索引，-1表示无示例选中
const selectedIndex = ref(0);
const val = ref<any>(demos[0].value);
const result = ref<boolean | null>(null);

// 校验函数
function checkIsObject() {
  result.value = isObject(val.value);
}

// 点击示例按钮
function selectDemo(index: number) {
  selectedIndex.value = index;
  val.value = demos[index].value;
  checkIsObject(); // 选示例时自动校验
}

// 监听示例变化自动校验
watch(val, () => {
  checkIsObject();
});

// 页面加载时自动校验默认示例
onMounted(() => {
  checkIsObject();
});

const resultText = computed(() =>
  result.value === null
    ? "请选择示例"
    : `isObject(${typeof val.value}) = ${result.value}`
);
</script>

<template>
  <n-card title="判断是否为普通对象（非null，非数组） - 多示例演示">
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
