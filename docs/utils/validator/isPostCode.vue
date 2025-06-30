<script setup lang="ts">
import { ref, computed, watch, onMounted } from "vue";
import { isPostCode } from "buzzts";

type DemoItem = { label: string; value: string | number };

const demos: DemoItem[] = [
  { label: "合法邮编", value: "100000" },
  { label: "合法邮编（数字）", value: 200000 },
  { label: "非法邮编", value: "ABCDE" },
  { label: "短数字", value: "123" },
  { label: "空字符串", value: "" },
];

const selectedIndex = ref(0);
const val = ref<string | number>(demos[0].value);
const result = ref<boolean | null>(null);

function checkIsPostCode() {
  result.value = isPostCode(val.value);
}

function selectDemo(index: number) {
  selectedIndex.value = index;
  val.value = demos[index].value;
  checkIsPostCode();
}

watch(val, () => {
  checkIsPostCode();
});

onMounted(() => {
  checkIsPostCode();
});

const resultText = computed(() =>
  result.value === null
    ? "请输入邮政编码或选择示例"
    : `isPostCode("${val.value}") = ${result.value}`
);
</script>

<template>
  <n-card title="大陆邮政编码校验 - 多示例演示">
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

      <n-input v-model:value="val" placeholder="请输入邮政编码" />

      <n-button type="primary" @click="checkIsPostCode">校验</n-button>

      <n-gradient-text v-if="result !== null" type="info" style="margin-top: 12px;">
        {{ resultText }}
      </n-gradient-text>
      <n-text v-else style="margin-top: 12px;">请输入邮政编码或选择示例</n-text>
    </n-space>
  </n-card>
</template>
