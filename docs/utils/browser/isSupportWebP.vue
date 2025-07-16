<script lang="ts">
import { ref, onMounted } from 'vue';
import { isSupportWebP } from 'buzzts';

export default {
  setup() {
    // 结果响应式变量，null 表示检测中
    const result = ref<boolean | null>(null);

    // 运行检测函数
    function check() {
      result.value = null;
      // 模拟异步检测，实际函数是同步的，但保持一致性
      setTimeout(() => {
        result.value = isSupportWebP();
      }, 0);
    }

    onMounted(() => {
      check();
    });

    return {
      result,
      check,
    };
  },
};
</script>

<template>
  <n-space vertical size="large" style="max-width: 600px; margin: auto;">
    <n-title depth="3" style="margin-bottom: 24px;">isSupportWebP 演示</n-title>

    <n-text style="margin-bottom: 16px;">
      当前浏览器是否支持 WebP 图片格式：<strong>{{ result === null ? '检测中...' : (result ? '支持' : '不支持') }}</strong>
    </n-text>

    <n-button  type="primary" @click="check">重新检测</n-button>
  </n-space>
</template>