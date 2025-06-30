<script setup lang="ts">
import { ref, computed, watch, onMounted } from "vue";
import { isHasEmoji } from "buzzts";

type DemoItem = { label: string; value: string };

const demos: DemoItem[] = [
  { label: "包含emoji", value: "Hello 😊" },
  { label: "无emoji", value: "Hello World" },
  { label: "纯emoji", value: "👍🔥🎉" },
  { label: "空字符串", value: "" },
  { label: "特殊符号", value: "@#$%^&*" },
];

// 当前选中示例索引，-1表示无示例选中
const selectedIndex = ref(0);
const val = ref(demos[0].value);
const result = ref<boolean | null>(null);

function checkIsHasEmoji() {
  result.value = isHasEmoji(val.value);
}

function selectDemo(index: number) {
  selectedIndex.value = index;
  val.value = demos[index].value;
  checkIsHasEmoji();
}

watch(val, () => {
  checkIsHasEmoji();
});

onMounted(() => {
  checkIsHasEmoji();
});

const resultText = computed(() =>
  result.value === null
    ? "请输入字符串或选择示例"
    : `isHasEmoji("${val.value}") = ${result.value}`
);
</script>

<template>
  <n-card title="是否包含emoji表情 - 多示例演示">
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

      <n-input v-model:value="val" placeholder="请输入字符串" />

      <n-button type="primary" @click="checkIsHasEmoji">校验</n-button>

      <n-gradient-text v-if="result !== null" type="info" style="margin-top: 12px;">
        {{ resultText }}
      </n-gradient-text>
      <n-text v-else style="margin-top: 12px;">请输入字符串或选择示例</n-text>
    </n-space>
  </n-card>
</template>
