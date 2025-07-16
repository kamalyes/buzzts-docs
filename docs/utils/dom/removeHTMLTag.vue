<template>
  <n-card title="移除HTML标签">
    <n-space vertical>
      <n-input
        type="textarea"
        v-model:value="htmlString"
        placeholder="输入包含HTML的字符串"
        style="width: 100%;"
        :rows="3"
      />
      <n-space wrap>
        <n-button type="primary" @click="removeTags">移除标签</n-button>
      </n-space>
      <n-gradient-text type="info" v-if="plainText !== ''">
        纯文本: {{ plainText }}
      </n-gradient-text>
      <n-text v-else style="margin-top: 12px;">纯文本为空</n-text>
    </n-space>
  </n-card>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import { removeHTMLTag } from 'buzzts';

// 定义响应式变量
const htmlString = ref('<p>Hello <b>World</b></p>');
const plainText = ref('');

// 定义移除标签的函数
const removeTags = () => {
  plainText.value = removeHTMLTag(htmlString.value);
};
</script>

<style scoped>
/* 可以根据需要添加样式 */
</style>
