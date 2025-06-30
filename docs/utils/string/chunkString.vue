<script setup lang="ts">
import { ref, computed, watch, onMounted } from "vue";
import { chunkString } from "buzzts";

type DemoItem = {
  label: string;
  str: string;
  chunkSize: number;
};

const demos: DemoItem[] = [
  { label: "字符串长度5，块大小3", str: "abcde", chunkSize: 3 },
  { label: "字符串长度26，块大小5", str: "abcdefghijklmnopqrstuvwxyz", chunkSize: 5 },
  { label: "空字符串", str: "", chunkSize: 1 },
  { label: "字符串长度7，块大小2", str: "1234567", chunkSize: 2 },
];

const selectedIndex = ref(0);
const str = ref(demos[0].str);
const chunkSize = ref(demos[0].chunkSize);
const result = ref<string[] | null>(null);
const errorMsg = ref<string>("");

function tryChunkString() {
  errorMsg.value = "";
  try {
    result.value = chunkString(str.value, chunkSize.value);
  } catch (error: any) {
    result.value = null;
    errorMsg.value = error.message || "未知错误";
  }
}

function selectDemo(index: number) {
  selectedIndex.value = index;
  str.value = demos[index].str;
  chunkSize.value = demos[index].chunkSize;
  tryChunkString();
}

watch([str, chunkSize], () => {
  tryChunkString();
});

onMounted(() => {
  tryChunkString();
});

const resultText = computed(() => {
  if (errorMsg.value) return `错误: ${errorMsg.value}`;
  if (!result.value) return "请设置字符串和块大小";
  return JSON.stringify(result.value);
});
</script>

<template>
  <n-card title="chunkString - 字符串分块演示">
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

      <n-form-item label="输入字符串">
        <n-input v-model:value="str" placeholder="请输入字符串" />
      </n-form-item>

      <n-form-item label="块大小">
        <n-input-number v-model:value="chunkSize" :min="1" />
      </n-form-item>

      <n-button type="primary" @click="tryChunkString">分块</n-button>

      <n-gradient-text type="info" style="margin-top: 12px;">
        {{ resultText }}
      </n-gradient-text>
    </n-space>
  </n-card>
</template>
