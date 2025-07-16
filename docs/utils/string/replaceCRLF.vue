<script setup lang="ts">
import { ref, computed } from "vue";
import { replaceCRLF } from 'buzzts';

const inputText = ref("Hello,\nWorld!\rThis is a test.");
const replacementString = ref('<br/>');

// 计算替换结果
const replacedResult = computed(() => replaceCRLF(inputText.value, replacementString.value));
</script>

<template>
  <n-card title="回车换行符替换">
    <n-divider>输入文本</n-divider>
    <div>
      <n-input
        v-model:value="inputText"
        type="textarea"
        rows="4"
        style="width: 100%;"
        placeholder="请输入文本..."
      />
    </div>
    <div>
      <strong>替换字符串：</strong>
      <n-input
        v-model:value="replacementString"
        style="width: 100%;"
        placeholder="请输入替换字符串..."
      />
    </div>
    <n-divider>替换结果</n-divider>
    <div v-html="replacedResult"></div>
  </n-card>
</template>
