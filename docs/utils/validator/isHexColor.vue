<script setup lang="ts">
import { ref, computed, watch, onMounted } from "vue";
import { isHexColor } from "buzzts";

type DemoItem = { label: string; value: string };

const demos: DemoItem[] = [
  { label: "6位Hex", value: "#1a2b3c" },
  { label: "3位Hex", value: "#abc" },
  { label: "无#前缀", value: "123456" },
  { label: "非法Hex", value: "#123abz" },
  { label: "空字符串", value: "" },
  { label: "大写Hex", value: "#ABCDEF" },
];

const selectedIndex = ref(0);
const val = ref(demos[0].value);
const result = ref<boolean | null>(null);

function checkIsHexColor() {
  result.value = isHexColor(val.value);
}

function selectDemo(index: number) {
  selectedIndex.value = index;
  val.value = demos[index].value;
  checkIsHexColor();
}

watch(val, () => {
  checkIsHexColor();
});

onMounted(() => {
  checkIsHexColor();
});

const resultText = computed(() =>
  result.value === null
    ? "请输入颜色字符串或选择示例"
    : `isHexColor("${val.value}") = ${result.value}`
);
</script>

<template>
  <n-card title="十六进制颜色校验 - 多示例演示">
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

      <n-input v-model:value="val" placeholder="请输入颜色字符串" />

      <n-button type="primary" @click="checkIsHexColor">校验</n-button>

      <n-gradient-text v-if="result !== null" type="info" style="margin-top: 12px;">
        {{ resultText }}
      </n-gradient-text>
      <n-text v-else style="margin-top: 12px;">请输入颜色字符串或选择示例</n-text>
    </n-space>
  </n-card>
</template>
