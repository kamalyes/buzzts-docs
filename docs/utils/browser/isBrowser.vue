<script lang="ts">
import { ref } from 'vue';
import { isBrowser } from 'buzzts';

export default {
  setup() {
    // 结果响应式变量，默认检测一次
    const result = ref(isBrowser());

    // 点击按钮重新检测
    function check() {
      result.value = isBrowser();
    }

    return {
      result,
      check,
    };
  },
};
</script>

<template>
  <n-space vertical size="large" style="max-width: 600px; margin: auto;">
    <n-title depth="3" style="margin-bottom: 24px;">isBrowser 演示</n-title>

    <n-text style="margin-bottom: 16px;">
      当前环境是否为浏览器：<strong>{{ result ? '是浏览器环境' : '非浏览器环境' }}</strong>
    </n-text>
  </n-space>
</template>