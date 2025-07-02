<script setup lang="ts">
// 引入 Vue 的响应式和生命周期函数
import { ref, onMounted, onBeforeUnmount } from 'vue';
// 引入 buzzts 的 Fullscreen 类，用于全屏控制
import { Fullscreen } from 'buzzts';

// 绑定内容区域 DOM 元素的引用
const contentRef = ref<HTMLElement | null>(null);

// 声明两个 Fullscreen 实例变量，分别管理内容区域和整体页面全屏
let contentFullscreen: Fullscreen | null = null;
let pageFullscreen: Fullscreen | null = null;

// 响应式变量，表示内容区域和整体页面是否处于全屏状态
const isContentFullscreen = ref(false);
const isPageFullscreen = ref(false);

// 加载状态，防止多次点击导致重复请求
const isLoadingContent = ref(false);
const isLoadingPage = ref(false);

/**
 * 初始化两个 Fullscreen 实例
 * 绑定对应的 DOM 元素，并监听全屏状态变化以同步响应式状态
 */
const initFullscreen = () => {
  // 初始化内容区域全屏实例
  if (contentRef.value && !contentFullscreen) {
    contentFullscreen = new Fullscreen(contentRef.value);
    // 监听内容区域全屏状态变化，更新 isContentFullscreen
    contentFullscreen.onChange(full => {
      isContentFullscreen.value = full;
    });
    // 组件初始化时同步当前状态
    isContentFullscreen.value = contentFullscreen.isFullscreen();
  }

  // 初始化整体页面全屏实例，绑定 document.documentElement（整个页面根元素）
  if (!pageFullscreen) {
    pageFullscreen = new Fullscreen(document.documentElement);
    // 监听整体页面全屏状态变化，更新 isPageFullscreen
    pageFullscreen.onChange(full => {
      isPageFullscreen.value = full;
    });
    // 组件初始化时同步当前状态
    isPageFullscreen.value = pageFullscreen.isFullscreen();
  }
};

// 组件挂载时初始化全屏实例
onMounted(() => {
  initFullscreen();
});

// 组件卸载时销毁全屏实例，释放资源，避免内存泄漏
onBeforeUnmount(() => {
  contentFullscreen?.destroy();
  contentFullscreen = null;
  pageFullscreen?.destroy();
  pageFullscreen = null;
});

/**
 * 进入内容区域全屏
 * 触发时设置加载状态，调用 Fullscreen 实例的 enter 方法
 * 捕获异常并打印错误，操作结束后取消加载状态
 */
const enterContentFullscreen = async () => {
  if (!contentFullscreen) return;
  isLoadingContent.value = true;
  try {
    await contentFullscreen.enter();
  } catch (e) {
    console.error('内容区域全屏失败', e);
  } finally {
    isLoadingContent.value = false;
  }
};

/**
 * 进入整体页面全屏
 * 逻辑同上，但操作整体页面的 Fullscreen 实例
 */
const enterPageFullscreen = async () => {
  if (!pageFullscreen) return;
  isLoadingPage.value = true;
  try {
    await pageFullscreen.enter();
  } catch (e) {
    console.error('整体页面全屏失败', e);
  } finally {
    isLoadingPage.value = false;
  }
};

/**
 * 退出整体页面全屏
 * 仅整体页面全屏有退出按钮，内容区域全屏通过 ESC 等系统方式退出
 */
const exitPageFullscreen = async () => {
  if (!pageFullscreen) return;
  isLoadingPage.value = true;
  try {
    await pageFullscreen.exit();
  } catch (e) {
    console.error('退出整体页面全屏失败', e);
  } finally {
    isLoadingPage.value = false;
  }
};
</script>

<template>
  <naive-theme>
    <n-card title="多入口全屏示例">
      <!-- 内容区域，绑定 ref 用于全屏操作 -->
      <div
        ref="contentRef"
        style="
          width: 25vw;              /* 初始宽度，方便演示 */
          height: 23vh;             /* 初始高度 */
          background: white;        /* 背景色，避免全屏黑屏 */
          overflow: auto;           /* 内容溢出可滚动 */
          border: 1px solid #ddd;   /* 边框样式 */
          padding: 16px;            /* 内边距 */
          box-sizing: border-box;   /* 盒模型包含边框和内边距 */
          margin-bottom: 16px;      /* 底部外边距 */
        "
      >
        <p>这里是内容区域的主体内容，进入内容区域全屏时会放大到全屏。</p>
        <p>退出内容区域全屏只能通过 ESC 键或系统手势操作。</p>
        <p style="margin-top: 8px;">
          <strong>状态：</strong><br />
          内容区域全屏：{{ isContentFullscreen ? '是' : '否' }}<br />
        </p>
      </div>

      <!-- 只显示进入内容区域全屏按钮 -->
      <n-space style="margin-bottom: 24px;">
        <n-button
          type="primary"
          @click="enterContentFullscreen"
          :loading="isLoadingContent"
          :disabled="isLoadingContent || isContentFullscreen"
        >
          内容区域进入全屏
        </n-button>
      </n-space>

      <n-divider />

      <!-- 整体页面全屏控制按钮 -->
      <p>整体页面全屏：</p>
      <n-space>
        <n-button
          type="primary"
          @click="enterPageFullscreen"
          :loading="isLoadingPage"
          :disabled="isLoadingPage || isPageFullscreen"
        >
          整体页面进入全屏
        </n-button>
        <n-button
          @click="exitPageFullscreen"
          :disabled="isLoadingPage || !isPageFullscreen"
        >
          整体页面退出全屏
        </n-button>
      </n-space>

      <!-- 显示整体页面全屏状态 -->
      <p style="margin-top: 16px;">
        <strong>状态：</strong><br />
        整体页面全屏：{{ isPageFullscreen ? '是' : '否' }}
      </p>
    </n-card>
  </naive-theme>
</template>
