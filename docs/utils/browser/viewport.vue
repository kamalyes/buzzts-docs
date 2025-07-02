<script lang="ts" setup>
import { reactive, onMounted, onBeforeUnmount } from 'vue';
import { Viewport } from 'buzzts';

// 创建响应式 viewport 实例
const viewport = reactive(new Viewport());

// 监听窗口尺寸变化时刷新并打印
function onResize() {
  // 这里 reactive 会自动更新 width 和 height
  console.log('窗口尺寸变化:', viewport.size());
}

// 手动刷新尺寸
function refreshSize() {
  viewport.refresh();
}

onMounted(() => {
  viewport.onResize(onResize);
});

onBeforeUnmount(() => {
  viewport.offResize();
});
</script>

<template>
  <n-space vertical size="large" style="max-width: 600px; margin: auto;">
    <n-title depth="3" style="margin-bottom: 24px;">Viewport 视口尺寸工具类演示</n-title>

    <n-text style="margin-bottom: 12px;">
      当前视口宽度：<strong>{{ viewport.width }}</strong> px
    </n-text>
    <n-text style="margin-bottom: 12px;">
      当前视口高度：<strong>{{ viewport.height }}</strong> px
    </n-text>
    <n-text style="margin-bottom: 24px;">
      当前视口尺寸对象：
      <code>{{ JSON.stringify(viewport.size()) }}</code>
    </n-text>

    <n-button @click="refreshSize" type="primary" style="margin-bottom: 24px;">手动刷新尺寸</n-button>

    <n-text>
      <strong>监听窗口尺寸变化事件：</strong>当窗口尺寸变化时，自动刷新视口尺寸并显示最新值。
    </n-text>
  </n-space>
</template>
