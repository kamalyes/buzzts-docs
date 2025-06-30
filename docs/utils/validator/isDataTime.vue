<script setup lang="ts">
import { ref, computed, watch, onMounted } from "vue";
import { isDataTime } from "buzzts";

type DemoItem = { label: string; value: string };

const demos: DemoItem[] = [
  { label: "标准时间", value: "2023-06-23 16:52:15" },
  { label: "无时间部分", value: "2023-06-23" },
  { label: "无秒数", value: "2023-06-23 16:52" },
  { label: "非法格式", value: "2023/06/23" },
  { label: "空字符串", value: "" },
  { label: "随机字符串", value: "abc123" },
];

// 当前选中示例索引，-1表示无示例选中
const selectedIndex = ref(0);
const val = ref(demos[0].value);
const result = ref<boolean | null>(null);

function checkIsDataTime() {
  result.value = isDataTime(val.value);
}

function selectDemo(index: number) {
  selectedIndex.value = index;
  val.value = demos[index].value;
  checkIsDataTime();
}

watch(val, () => {
  checkIsDataTime();
});

onMounted(() => {
  checkIsDataTime();
});

const resultText = computed(() =>
  result.value === null
    ? "请输入时间字符串或选择示例"
    : `isDataTime("${val.value}") = ${result.value}`
);
</script>

<template>
  <n-card title="简单时间格式校验 - 多示例演示">
    <n-space vertical size="large">
      <n-space wrap>
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

      <n-input v-model:value="val" placeholder="请输入时间字符串" />

      <n-button type="primary" @click="checkIsDataTime">校验</n-button>

      <n-gradient-text v-if="result !== null" type="info" style="margin-top: 12px;">
        {{ resultText }}
      </n-gradient-text>
      <n-text v-else style="margin-top: 12px;">请输入时间字符串或选择示例</n-text>
    </n-space>
  </n-card>
</template>
