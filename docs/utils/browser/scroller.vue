<script setup lang="ts">
// 引入 Vue 响应式和生命周期函数
import { ref, onMounted, onBeforeUnmount } from 'vue';
// 引入 buzzts 的 Scroller 类 & 缓动函数类型和随机数函数
import { Scroller, EasingFunction, randInt } from 'buzzts';

// ---------- 响应式变量 ----------

// 标记当前是否在滚动中
const isScrolling = ref(false);
// 滚动进度，范围 0~1
const scrollProgress = ref(0);
// 生成随机内容数量，演示用
const contextCount = ref(randInt(30, 100));

// 纵向和横向滚动容器的 DOM 引用
const containerRef = ref<HTMLElement | null>(null);
const containerRefHorizontal = ref<HTMLElement | null>(null);

// 分别保存纵向和横向的 Scroller 实例
const scrollerVertical = ref<Scroller | null>(null);
const scrollerHorizontal = ref<Scroller | null>(null);

// 动画时长，单位毫秒，滑块控制，默认 800ms
const duration = ref(800);

// ---------- 缓动函数列表 ----------
// key 为名称，value 为对应的缓动函数
const easingFunctions: Record<string, EasingFunction> = {
  easeInOutQuad: t => (t < 0.5 ? 2 * t * t : -1 + (4 - 2 * t) * t),
  linear: t => t,
  easeOutCubic: t => 1 - Math.pow(1 - t, 3),
  easeInCubic: t => t * t * t,
};
// 当前选中的缓动函数名称，双向绑定到下拉框
const selectedEasing = ref('easeInOutQuad');

// ---------- 生命周期钩子 ----------

// 组件挂载完成后，初始化两个 Scroller 实例
onMounted(() => {
  // 如果纵向容器存在，创建纵向滚动实例
  if (containerRef.value) {
    scrollerVertical.value = new Scroller(containerRef.value);
  }
  // 如果横向容器存在，创建横向滚动实例
  if (containerRefHorizontal.value) {
    scrollerHorizontal.value = new Scroller(containerRefHorizontal.value);
  }

  // 定义一个循环函数，持续监听滚动状态和进度
  const updateStatus = () => {
    // 判断两个实例是否有滚动动画在进行
    const scrollingV = scrollerVertical.value?.isScrolling() ?? false;
    const scrollingH = scrollerHorizontal.value?.isScrolling() ?? false;
    // 只要有一个在滚动，就标记为滚动中
    isScrolling.value = scrollingV || scrollingH;

    // 优先显示纵向滚动进度，如果没有，则显示横向滚动进度
    if (scrollingV) {
      scrollProgress.value = scrollerVertical.value?.['progress'] ?? 0;
    } else if (scrollingH) {
      scrollProgress.value = scrollerHorizontal.value?.['progress'] ?? 0;
    } else {
      scrollProgress.value = 0;
    }

    // 如果仍在滚动，继续下一帧检测
    if (isScrolling.value) {
      requestAnimationFrame(updateStatus);
    }
  };

  // 启动首次状态检测
  requestAnimationFrame(updateStatus);
});

// 组件卸载前，取消所有滚动动画，释放资源
onBeforeUnmount(() => {
  scrollerVertical.value?.cancel();
  scrollerVertical.value = null;
  scrollerHorizontal.value?.cancel();
  scrollerHorizontal.value = null;
});

// ---------- 纵向滚动控制函数 ----------

// 滚动到顶部（纵向滚动条位置 0）
const scrollToTop = () => {
  if (!scrollerVertical.value) return;
  scrollerVertical.value.yTo(0, {
    duration: duration.value,
    easing: easingFunctions[selectedEasing.value], // 选中的缓动函数
  });
  requestAnimationFrame(checkScrollStatus);
};

// 滚动到底部（纵向滚动条最大值）
const scrollToBottom = () => {
  if (!containerRef.value || !scrollerVertical.value) return;
  // 计算最大滚动距离 = 内容高度 - 容器高度
  const maxScrollTop = containerRef.value.scrollHeight - containerRef.value.clientHeight;
  scrollerVertical.value.yTo(maxScrollTop, {
    duration: duration.value,
    easing: easingFunctions[selectedEasing.value],
  });
  requestAnimationFrame(checkScrollStatus);
};

// ---------- 横向滚动控制函数 ----------

// 滚动到最右侧（横向滚动条最大值）
const scrollToRight = () => {
  if (!containerRefHorizontal.value || !scrollerHorizontal.value) return;
  // 计算最大横向滚动距离 = 内容宽度 - 容器宽度
  const maxScrollLeft = containerRefHorizontal.value.scrollWidth - containerRefHorizontal.value.clientWidth;
  scrollerHorizontal.value.xTo(maxScrollLeft, {
    duration: duration.value,
    easing: easingFunctions[selectedEasing.value],
  });
  requestAnimationFrame(checkScrollStatus);
};

// 滚动回最左侧（横向滚动条位置 0）
const scrollToLeft = () => {
  if (!scrollerHorizontal.value) return;
  scrollerHorizontal.value.xTo(0, {
    duration: duration.value,
    easing: easingFunctions[selectedEasing.value],
  });
  requestAnimationFrame(checkScrollStatus);
};

// ---------- 其他控制函数 ----------

// 暂停所有滚动动画
const pauseScroll = () => {
  scrollerVertical.value?.pause();
  scrollerHorizontal.value?.pause();
};

// 恢复所有滚动动画
const resumeScroll = () => {
  scrollerVertical.value?.resume();
  scrollerHorizontal.value?.resume();
  requestAnimationFrame(checkScrollStatus);
};

// 取消所有滚动动画，重置状态
const cancelScroll = () => {
  scrollerVertical.value?.cancel();
  scrollerHorizontal.value?.cancel();
  isScrolling.value = false;
  scrollProgress.value = 0;
};

// ---------- 滚动状态检测函数 ----------
// 用于持续检测滚动状态和进度，配合 requestAnimationFrame 使用
function checkScrollStatus() {
  const scrollingV = scrollerVertical.value?.isScrolling() ?? false;
  const scrollingH = scrollerHorizontal.value?.isScrolling() ?? false;
  isScrolling.value = scrollingV || scrollingH;

  if (scrollingV) {
    scrollProgress.value = scrollerVertical.value?.['progress'] ?? 0;
  } else if (scrollingH) {
    scrollProgress.value = scrollerHorizontal.value?.['progress'] ?? 0;
  } else {
    scrollProgress.value = 0;
  }

  if (isScrolling.value) {
    requestAnimationFrame(checkScrollStatus);
  }
}
</script>

<template>
  <n-card title="平滑滚动示例（Scroller）增强版" style="width: 450px; margin: 20px auto;">
    <!-- 纵向滚动容器 -->
    <div
      ref="containerRef"
      style="
        height: 200px;
        overflow: auto;
        border: 1px solid #ccc;
        padding: 12px;
        box-sizing: border-box;
        user-select: text;
        background: #f9f9f9;
      "
    >
      <!-- 纵向示例内容 -->
      <div style="width: 100%;">
        <p v-for="i in contextCount" :key="i" style="margin: 4px 0;">
          纵向示例内容 {{ i }}
        </p>
      </div>
    </div>

    <!-- 横向滚动容器 -->
    <div
      ref="containerRefHorizontal"
      style="
        height: 70px;
        overflow-x: auto;
        border: 1px solid #ccc;
        padding: 12px;
        box-sizing: border-box;
        user-select: text;
        background: #f0f0f0;
        white-space: nowrap;
        margin-top: 20px;
      "
    >
      <!-- 横向示例内容，宽度超过容器宽度，触发横向滚动 -->
      <div
        style="
          width: 1200px;
          display: flex;
          gap: 8px;
          align-items: center;
          height: 100%;
        "
      >
        <p
          v-for="i in contextCount"
          :key="i"
          style="
            margin: 0;
            min-width: 100px;
            flex-shrink: 0;
            line-height: 1.4;
            background: #fff;
            padding: 3px;
            border-radius: 4px;
            box-shadow: 0 0 3px rgba(0, 0, 0, 0.1);
          "
        >
          横向示例内容 {{ i }}
        </p>
      </div>
    </div>
    
    <!-- 滑块控制动画时长 -->
    <n-space align="center" style="margin-bottom: 16px;">
      <label for="duration-range">动画时长 (ms): {{ duration }}</label>
      <input
        id="duration-range"
        type="range"
        min="100"
        max="10000"
        step="50"
        v-model="duration"
        style="width: 200px;"
      />
    </n-space>

    <!-- 缓动函数选择 -->
    <n-space style="margin: 16px 0;">
      <label for="easing-select">选择缓动函数：</label>
      <select id="easing-select" v-model="selectedEasing">
        <option v-for="(fn, name) in easingFunctions" :key="name" :value="name">{{ name }}</option>
      </select>
    </n-space>

    <!-- 控制按钮 -->
    <n-space style="margin-top: 16px; flex-wrap: wrap;">
      <n-button type="primary" @click="scrollToTop" :disabled="!containerRef">滚动到顶部</n-button>
      <n-button type="primary" @click="scrollToBottom" :disabled="!containerRef">滚动到底部</n-button>
      <n-button type="primary" @click="scrollToLeft" :disabled="!containerRefHorizontal">滚动到左侧</n-button>
      <n-button type="primary" @click="scrollToRight" :disabled="!containerRefHorizontal">滚动到右侧</n-button>
      <n-button @click="pauseScroll" :disabled="!isScrolling">暂停滚动</n-button>
      <n-button @click="resumeScroll" :disabled="isScrolling">恢复滚动</n-button>
      <n-button @click="cancelScroll" :disabled="!isScrolling">取消滚动</n-button>
    </n-space>

    <!-- 显示当前滚动状态和进度 -->
    <p style="margin-top: 12px;">
      <strong>滚动状态：</strong> {{ isScrolling ? '滚动中' : '空闲' }}
      <br />
      <strong>滚动进度：</strong> {{ (scrollProgress * 100).toFixed(1) }}%
    </p>
  </n-card>
</template>
