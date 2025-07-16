<script setup lang="ts">
import { ref, computed } from 'vue';
import { fileToBase64, base64ToImageFile } from 'buzzts'; 

// 定义状态变量
const fileName = ref('');
const fileContent = ref('');
const showModal = ref(false);

// 选择文件的函数
const selectFile = async () => {
  const fileInput = document.createElement('input');
  fileInput.type = 'file';
  fileInput.accept = 'image/*'; // 可根据需要调整文件类型
  fileInput.onchange = async (event) => {
    const target = event.target as HTMLInputElement; // 类型断言
    const file = target.files[0];
    if (file) {
      fileContent.value = await fileToBase64(file);
      showModal.value = true;
    }
  };
  fileInput.click();
};

// 上传文件的函数
const uploadFile = () => {
  const file = base64ToImageFile(fileContent.value, fileName.value);
  console.log('上传的文件:', file);
  // 这里可以添加上传文件的逻辑
};

// 处理模态框确认操作
const handleOk = () => {
  showModal.value = false;
};
</script>

<template>
  <n-card title="文件上传示例">
    <n-divider>选择文件</n-divider>
    <n-button type="primary" @click="selectFile">选择文件</n-button>
    
    <n-divider>文件名</n-divider>
    <n-input v-model:value="fileName" placeholder="请输入文件名" style="width: 100%;" />
    
    <n-button type="primary" @click="uploadFile">上传文件</n-button>

    <n-modal v-model:visible="showModal" title="文件内容" @ok="handleOk">
      <template #default>
        <p>文件内容：{{ fileContent }}</p>
      </template>
    </n-modal>
  </n-card>
</template>

<style scoped>
/* 可选样式 */
</style>
