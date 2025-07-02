<script setup lang="ts">
// 引入 Vue 的响应式和生命周期函数
import { ref, onMounted, onBeforeUnmount } from 'vue';
// 引入 buzzts 的 Fullscreen 类，用于全屏控制
import { Fullscreen, randColorRGB } from 'buzzts';

// 绑定内容区域 DOM 元素的引用
const contentRef = ref<HTMLElement | null>(null);
const videoRef = ref<HTMLVideoElement | null>(null);
const otherRef = ref<HTMLElement | null>(null);

// 声明Fullscreen 实例变量
const contentFullscreen = ref<Fullscreen | null>(null);
const pageFullscreen = ref<Fullscreen | null>(null);
const videoFullscreen = ref<Fullscreen | null>(null);
const otherFullscreen = ref<Fullscreen | null>(null);

// 响应式变量，表示内容区域和整体页面是否处于全屏状态
const isContentFullscreen = ref(false);
const isPageFullscreen = ref(false);
const isVideoFullscreen = ref(false);
const isOtherFullscreen = ref(false);

// 加载状态，防止多次点击导致重复请求
const isLoadingContent = ref(false);
const isLoadingPage = ref(false);
const isLoadingVideo = ref(false);
const isLoadingOther = ref(false);

// 生成随机 rgba 颜色，透明度0.8
function getRandomColor(): string {
  return randColorRGB([100, 200], [50, 150], [0, 100])
}


/**
 * 通用初始化 Fullscreen 实例函数
 * @param elementRef - 绑定的 DOM 引用
 * @param fullscreenInstanceRef - Fullscreen 实例变量引用（传入对象，用于赋值）
 * @param isFullscreenRef - 响应式全屏状态变量
 * @param useDefaultElement - 是否使用默认元素（如整体页面用 document.documentElement）
 */
function setupFullscreen(
  elementRef: typeof contentRef | null,
  fullscreenInstanceRef: typeof contentFullscreen,
  isFullscreenRef: typeof isContentFullscreen,
  useDefaultElement = false,
) {
  // 初始化整体页面全屏实例，绑定 document.documentElement（整个页面根元素）
  const el = useDefaultElement ? document.documentElement : elementRef?.value;
  if (el && !fullscreenInstanceRef.value) {
    fullscreenInstanceRef.value = new Fullscreen(el, true, getRandomColor());
    // 监听整体页面全屏状态变化，更新 isPageFullscreen
    fullscreenInstanceRef.value.onChange(full => {
      isFullscreenRef.value = full;
    });
    // 组件初始化时同步当前状态
    isFullscreenRef.value = fullscreenInstanceRef.value.isFullscreen();
  }
}

const initFullscreen = () => {
  setupFullscreen(contentRef, contentFullscreen, isContentFullscreen);
  setupFullscreen(null, pageFullscreen, isPageFullscreen, true);
  setupFullscreen(videoRef, videoFullscreen, isVideoFullscreen);
  setupFullscreen(otherRef, otherFullscreen, isOtherFullscreen);
};

// 组件挂载时初始化全屏实例
onMounted(() => {
  initFullscreen();
});

// 组件卸载时销毁全屏实例，释放资源，避免内存泄漏
onBeforeUnmount(() => {
  contentFullscreen.value?.destroy();
  contentFullscreen.value = null;
  pageFullscreen.value?.destroy();
  pageFullscreen.value = null;
  videoFullscreen.value?.destroy();
  videoFullscreen.value = null;
  otherFullscreen.value?.destroy();
  otherFullscreen.value = null;
});

/**
 * 全屏操作类型枚举
 */
enum FullscreenAction {
  Enter = 'enter',
  Exit = 'exit',
}

/**
 * 通用执行全屏操作函数
 * @param fullscreenRef - Fullscreen 实例的 ref
 * @param loadingRef - 对应的 loading 状态 ref
 * @param action - 全屏操作类型，使用 FullscreenAction 枚举，默认为 Enter
 * @param errorMsg - 失败时打印的错误信息前缀，默认为 '全屏操作失败'
 */
async function execFullscreenAction(
  fullscreenRef: typeof contentFullscreen,
  loadingRef: typeof isLoadingContent,
  action: FullscreenAction = FullscreenAction.Enter,
  errorMsg = '全屏操作失败'
): Promise<void> {
  if (!fullscreenRef.value) return;
  loadingRef.value = true;
  try {
    if (action === FullscreenAction.Enter) {
      await fullscreenRef.value.enter();
    } else if (action === FullscreenAction.Exit) {
      await fullscreenRef.value.exit();
    }
  } catch (e) {
    console.error(errorMsg, e);
  } finally {
    loadingRef.value = false;
  }
}

// 进入内容区域全屏
const enterContentFullscreen = () =>
  execFullscreenAction(contentFullscreen, isLoadingContent, FullscreenAction.Enter, '内容区域全屏失败');

// 进入整体页面全屏
const enterPageFullscreen = () =>
  execFullscreenAction(pageFullscreen, isLoadingPage, FullscreenAction.Enter, '整体页面全屏失败');
// 退出整体页面全屏
const exitPageFullscreen = () =>
  execFullscreenAction(pageFullscreen, isLoadingPage, FullscreenAction.Exit, '退出整体页面全屏失败');

// 进入视频全屏
const enterVideoFullscreen = () =>
  execFullscreenAction(videoFullscreen, isLoadingVideo, FullscreenAction.Enter, '视频全屏失败');

// 进入其他元素全屏
const enterOtherFullscreen = () =>
  execFullscreenAction(otherFullscreen, isLoadingOther, FullscreenAction.Enter, '其他元素全屏失败');

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

      <!-- 整体页面 -->
      <p>
        <strong>整体页面全屏状态：</strong> {{ isPageFullscreen ? '是' : '否' }}
      </p>
      <n-space style="margin-bottom: 24px;">
        <n-button
          type="primary"
          @click="enterPageFullscreen"
          :loading="isLoadingPage"
          :disabled="isLoadingPage || isPageFullscreen"
        >
          整体页面进入全屏
        </n-button>
        <n-button
          type="info"
          @click="exitPageFullscreen"
          :loading="isLoadingPage"
          :disabled="isLoadingPage || !isPageFullscreen"
        >
          退出整体页面全屏
        </n-button>
      </n-space>

      <n-divider />

      <!-- video 元素 -->
      <div style="margin-bottom: 16px;">
        <video
          ref="videoRef"
          controls
          style="width: 25vw; height: 23vh; border: 1px solid #ddd;"
          src="https://www.w3schools.com/html/mov_bbb.mp4"
        ></video>
        <p style="margin-top: 8px;">
          <strong>视频全屏状态：</strong> {{ isVideoFullscreen ? '是' : '否' }}
        </p>
        <n-button
          type="primary"
          @click="enterVideoFullscreen"
          :loading="isLoadingVideo"
          :disabled="isLoadingVideo || isVideoFullscreen"
        >
          视频进入全屏
        </n-button>
      </div>

      <n-divider />

      <!-- 其他元素示例（图片） -->
      <div
        ref="otherRef"
        style="
          width: 25vw;
          height: 23vh;
          background: url('https://picsum.photos/400/300') no-repeat center/cover;
          border: 1px solid #ddd;
          margin-bottom: 8px;
        "
      ></div>
      <p>
        <strong>图片区域全屏状态：</strong> {{ isOtherFullscreen ? '是' : '否' }}
      </p>
      <n-button
        type="primary"
        @click="enterOtherFullscreen"
        :loading="isLoadingOther"
        :disabled="isLoadingOther || isOtherFullscreen"
      >
        图片区域进入全屏
      </n-button>
    </n-card>
  </naive-theme>
</template>
