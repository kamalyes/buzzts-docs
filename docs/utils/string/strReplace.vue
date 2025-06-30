<script setup lang="ts">
import { ref, computed, watch, onMounted } from "vue";
import { strReplace } from "buzzts";

type DemoItem = {
  label: string;
  str: string;
  start: number;
  end: number;
  replacement: string;
};

const demos: DemoItem[] = [
  { label: "替换中间4个字符为 '*'", str: "123756789", start: 3, end: 6, replacement: "*" },
  { label: "负索引替换4个字符为 '#'", str: "123756789", start: -6, end: -3, replacement: "#" },
  { label: "替换多字符", str: "abcdefg", start: 2, end: 5, replacement: "XY" },
  { label: "删除区间字符", str: "abcdefg", start: 2, end: 5, replacement: "" },
];

const selectedIndex = ref(0);
const str = ref(demos[0].str);
const start = ref(demos[0].start);
const end = ref(demos[0].end);
const replacement = ref(demos[0].replacement);
const result = ref<string>("");

function doReplace() {
  result.value = strReplace(str.value, start.value, end.value, replacement.value);
}

function selectDemo(index: number) {
  selectedIndex.value = index;
  str.value = demos[index].str;
  start.value = demos[index].start;
  end.value = demos[index].end;
  replacement.value = demos[index].replacement;
  doReplace();
}

watch([str, start, end, replacement], () => {
  doReplace();
});

onMounted(() => {
  doReplace();
});

const resultText = computed(() => `strReplace("${str.value}", ${start.value}, ${end.value}, "${replacement.value}") = "${result.value}"`);
</script>

<template>
  <n-card title="strReplace - 字符串指定区间替换演示">
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

      <n-form-item label="原字符串">
        <n-input v-model:value="str" placeholder="请输入原始字符串" />
      </n-form-item>

      <n-form-item label="开始索引">
        <n-input-number v-model:value="start" :min="-str.length" :max="str.length" />
      </n-form-item>

      <n-form-item label="结束索引">
        <n-input-number v-model:value="end" :min="-str.length" :max="str.length" />
      </n-form-item>

      <n-form-item label="替换字符串">
        <n-input v-model:value="replacement" placeholder="替换字符串，空字符串表示删除" />
      </n-form-item>

      <n-button type="primary" @click="doReplace">替换</n-button>

      <n-gradient-text type="info" style="margin-top: 12px;">
        {{ resultText }}
      </n-gradient-text>
    </n-space>
  </n-card>
</template>
