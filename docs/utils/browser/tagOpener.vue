<script lang="ts">
import { ref, watch } from 'vue';
import { TagOpener } from 'buzzts'; // 直接引入你的TagOpener类

export default {
  setup() {
    // URL 输入框绑定的响应式变量，默认示例地址
    const url = ref('https://www.example.com');

    // 打开方式，默认为新标签页
    const openType = ref<number>(TagOpener.OpenType.NEW_TAB);

    // 弹窗参数，包含宽度、高度和是否模态，默认值
    const popupOptions = ref({
      width: 800,
      height: 600,
      modal: false,
    });

    // 弹窗关闭状态标记，true 表示弹窗已关闭
    const popupClosed = ref(false);

    // 内嵌iframe容器的DOM引用
    const embedContainer = ref<HTMLElement | null>(null);

    // 创建TagOpener实例
    const opener = new TagOpener();

    /**
     * 打开页面函数，根据不同打开方式调用TagOpener.open
     */
    function openPage() {
      // 打开时重置弹窗关闭状态
      popupClosed.value = false;

      // 定义回调函数，处理打开和关闭事件
      const callbacks = {
        onOpen(win: Window | null) {
          // 如果打开失败且不是内嵌方式，提示用户
          if (!win && openType.value !== TagOpener.OpenType.EMBEDDED) {
            alert('页面打开被拦截或失败');
          }
        },
        onClose() {
          // 弹窗关闭时，设置状态为已关闭
          popupClosed.value = true;
        },
      };

      // 根据打开方式分别处理
      if (openType.value === TagOpener.OpenType.EMBEDDED) {
        // 内嵌iframe方式，需确认容器已准备好
        if (embedContainer.value) {
          opener.open(url.value, openType.value, undefined, callbacks, embedContainer.value);
        } else {
          alert('内嵌容器未准备好');
        }
      } else if (openType.value === TagOpener.OpenType.POPUP) {
        // 弹窗方式，传递弹窗参数
        opener.open(url.value, openType.value, popupOptions.value, callbacks);
      } else {
        // 其他方式（新标签页等），不传额外参数
        opener.open(url.value, openType.value, undefined, callbacks);
      }
    }

    /**
     * 监听打开方式切换时调用，重置相关状态和UI
     * @param newType 新选中的打开方式
     */
    function handleOpenTypeChange(newType: number) {
      // 切换时重置弹窗关闭状态
      popupClosed.value = false;

      // 如果切换到非弹窗方式，重置弹窗参数为默认
      if (newType !== TagOpener.OpenType.POPUP) {
        popupOptions.value = {
          width: 800,
          height: 600,
          modal: false,
        };
      }

      // 如果切换到非内嵌iframe方式，清空内嵌容器内容，避免残留iframe
      if (newType !== TagOpener.OpenType.EMBEDDED && embedContainer.value) {
        embedContainer.value.innerHTML = '';
      }
    }

    // 额外监听openType变量变化，确保所有修改都能触发清理逻辑
    watch(openType, (newType) => {
      handleOpenTypeChange(newType);
    });

    return {
      url,
      openType,
      popupOptions,
      popupClosed,
      embedContainer,
      TagOpener,
      openPage,
      handleOpenTypeChange,
    };
  },
};
</script>

<template>
  <n-space vertical size="large" style="max-width: 600px; margin: auto;">
    <n-title depth="3" style="margin-bottom: 24px;">TagOpener 演示</n-title>

    <n-form
      label-placement="left"
      label-width="60px"
      label-align="right"
      size="medium"
      :inline="false"
      :show-feedback="false"
      style="margin-bottom: 24px;"
    >
      <!-- URL 输入 -->
      <n-form-item label="URL：" style="margin-bottom: 16px;">
        <n-input v-model:value="url" placeholder="https://example.com" clearable />
      </n-form-item>

      <!-- 打开方式选择 -->
      <n-form-item label="打开方式：" style="margin-bottom: 16px;">
        <n-select
          v-model:value="openType"
          :options="[
            { label: '新标签页', value: TagOpener.OpenType.NEW_TAB },
            { label: '弹窗', value: TagOpener.OpenType.POPUP },
            { label: '内嵌iframe', value: TagOpener.OpenType.EMBEDDED }
          ]"
          clearable
          @update:value="handleOpenTypeChange"
        />
      </n-form-item>

      <!-- 弹窗参数区，仅当选择“弹窗”时显示 -->
      <template v-if="openType === TagOpener.OpenType.POPUP">
        <n-divider style="margin: 24px 0;" />
        <n-title depth="4" style="margin-bottom: 16px;">弹窗参数（可选）</n-title>

        <n-form-item label="宽度(px)：" style="margin-bottom: 16px;">
          <n-input-number
            v-model:value="popupOptions.width"
            :min="100"
            :step="10"
          />
        </n-form-item>

        <n-form-item label="高度(px)：" style="margin-bottom: 16px;">
          <n-input-number
            v-model:value="popupOptions.height"
            :min="100"
            :step="10"
          />
        </n-form-item>

        <n-form-item label="模态弹窗：" style="margin-bottom: 16px;">
          <n-switch v-model:value="popupOptions.modal" />
        </n-form-item>
      </template>

      <!-- 打开页面按钮 -->
      <n-form-item style="margin-top: 24px;">
        <n-button type="primary" @click="openPage" block>打开页面</n-button>
      </n-form-item>

      <!-- 弹窗关闭提示 -->
      <n-form-item v-if="popupClosed" style="margin-top: 12px;">
        <n-text type="error">弹窗已关闭</n-text>
      </n-form-item>
    </n-form>

    <!-- 内嵌iframe容器，仅当选择“内嵌iframe”时显示 -->
    <div
      v-if="openType === TagOpener.OpenType.EMBEDDED"
      ref="embedContainer"
      style="
        margin-top: 20px;
        height: 400px;
        border: 1px solid var(--n-color-border);
        border-radius: var(--n-border-radius);
        overflow: hidden;
      "
    ></div>
  </n-space>
</template>