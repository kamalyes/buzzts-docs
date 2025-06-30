<script setup lang="ts">
import { ref, computed, watch, onMounted } from "vue";
import { isNumberEnUnderscores } from "buzzts";

type DemoItem = { label: string; value: string };

const demos: DemoItem[] = [
  { label: "数字+英文+下划线", value: "abc_123" },
  { label: "数字+英文", value: "abc123" },
  { label: "纯数字", value: "123456" },
  { label: "纯英文", value: "abcdef" },
  { label: "含破折号", value: "abc-123" },
  { label: "含空格", value: "abc 123" },
  { label: "空字符串", value: "" },
];

const selectedIndex = ref(0);
const val = ref(demos[0].value);
const result = ref<boolean | null>(null);

function check() {
  result.value = isNumberEnUnderscores(val.value);
}

function selectDemo(index: number) {
  selectedIndex.value = index;
  val.value = demos[index].value;
  check();
}

watch(val, () => {
  check();
});

onMounted(() => {
  check();
});

const resultText = computed(() =>
  result.value === null
    ? "请输入字符串或选择示例"
    : `isNumberEnUnderscores(${val.value}) = ${result.value}`
);
</script>

<template>
  <n-card title="数字、英文及下划线校验 - 多示例演示">
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
      <n-button type="primary" @click="check">校验</n-button>
      <n-gradient-text v-if="result !== null" type="info" style="margin-top: 12px;">
        {{ resultText }}
      </n-gradient-text>
      <n-text v-else style="margin-top: 12px;">请输入字符串或选择示例</n-text>
    </n-space>
  </n-card>
</template>
