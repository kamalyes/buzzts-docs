<template>
  <n-card title="Logger 示例">
    <n-space vertical>
      <n-space wrap>
        <n-button type="info" @click="log('debug')">记录调试信息</n-button>
        <n-button type="primary" @click="log('info')">记录普通信息</n-button>
        <n-button type="warning" @click="log('warn')">记录警告信息</n-button>
        <n-button type="error" @click="log('error')">记录错误信息</n-button>
        <n-button type="success" @click="log('success')">记录成功信息</n-button>
        <n-button type="primary" @click="logTable">记录表格数据</n-button>
        <n-button type="info" @click="logObject">记录对象数据</n-button>
      </n-space>
      <n-space wrap>
        <n-button type="error" @click="clearLogs">清除日志</n-button>
        <n-button type="info" @click="startGroup">开始分组</n-button>
        <n-button type="primary" @click="endGroup">结束分组</n-button>
        <n-button type="success" @click="startCollapsedGroup">开始折叠分组</n-button>
      </n-space>
    </n-space>
    <div v-if="storedLogs.length">
      <h3>已记录的日志:</h3>
      <ul>
        <li v-for="(log, index) in storedLogs" :key="index">{{ log }}</li>
      </ul>
    </div>
  </n-card>
</template>

<script setup lang="ts">
import { ref, onMounted, computed } from 'vue';
import { Logger, randString, randInt, RandType } from 'buzzts';

const logger = ref<Logger | null>(null);
const storedLogs = ref<string[]>([]);

// 在组件挂载时初始化 Logger 实例
onMounted(() => {
  logger.value = new Logger({
    logLevel: 'debug',
    colors: true,
    emoji: true,
    timestamp: true,
    persistent: true, // 启用持久化
  });
  logger.value.clearLogs()
});

// 生成随机字符串
const generateRandomMessage = (level) => {
  return `随机${level}消息 - ${randString(randInt(15,30),RandType.CAPITAL| RandType.LOWERCASE| RandType.NUMBER| RandType.SPECIAL)}`;
};

// 统一的日志记录方法
const log = (level: 'debug' | 'info' | 'warn' | 'error' | 'success') => {
  if (logger.value) {
    const messageToLog = generateRandomMessage(level);
    logger.value[level](messageToLog);
    updateStoredLogs(); // 记录日志后更新存储的日志
  }
};

// 记录表格数据
const logTable = () => {
  if (logger.value) {
    const tableData = [
      { Name: "Alice", Age: 30, Job: "Engineer" },
      { Name: "Bob", Age: 25, Job: "Designer" },
      { Name: "Charlie", Age: 35, Job: "Teacher" },
    ];
    logger.value.table(tableData); // 使用 Logger 的 table 方法
    updateStoredLogs(); // 记录表格数据后更新存储的日志
  }
};

// 记录对象数据
const logObject = () => {
  if (logger.value) {
    const objData = { name: "Alice", age: 30, job: "Engineer" };
    logger.value.dir(objData); // 使用 Logger 的 dir 方法
    updateStoredLogs(); // 记录对象数据后更新存储的日志
  }
};

// 开始分组
const startGroup = () => {
  if (logger.value) {
    logger.value.group("示例分组");
  }
};

// 结束分组
const endGroup = () => {
  if (logger.value) {
    logger.value.groupEnd();
  }
};

// 开始折叠分组
const startCollapsedGroup = () => {
  if (logger.value) {
    logger.value.groupCollapsed("示例折叠分组");
  }
};

// 清除日志
const clearLogs = () => {
  if (logger.value) {
    logger.value.clearLogs(); // 清除日志
    storedLogs.value = []; // 清空显示的日志
  }
};

// 更新存储的日志
const updateStoredLogs = () => {
  const storedLogsData = JSON.parse(localStorage.getItem('logs') || '[]');
  storedLogs.value = storedLogsData; // 从 localStorage 获取日志
};

// 计算属性，自动获取已记录的日志
const displayedLogs = computed(() => {
  return storedLogs.value;
});
</script>

<style scoped>
/* 可以在这里添加样式 */
</style>
