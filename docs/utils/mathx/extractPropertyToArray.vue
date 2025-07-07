<script setup lang="ts">
import { ref, computed } from 'vue';
import { extractPropertyToArray } from 'buzzts'

interface Item {
  [key: string]: any; // 允许任意属性
}

const inputJson = ref<string>(JSON.stringify([{"id":1,"name":"Alice"}, {"id":2,"name":"Bob"}]));
const propertyKey = ref<string>('id');
const extractedKeys = ref<string[]>([]);
const excludeNil = ref<boolean>(true); // 用于控制开关的状态

const extractKeys = () => {
  try {
    const items: Item[] = JSON.parse(inputJson.value);
    extractedKeys.value = extractPropertyToArray(items, propertyKey.value, excludeNil.value);
  } catch (error) {
    alert('请输入有效的 JSON 格式数据！');
  }
};

const resultText = computed(() => {
  if (extractedKeys.value.length < 1) return "点击提取属性";
  return `extractPropertyToArray([${inputJson.value}], '${propertyKey.value}', ${excludeNil.value}) = ${extractedKeys.value}`;
});

</script>

<template>
  <div>
    <n-card title="提取属性示例">
      <n-space vertical>
        <div class="input-container">
          <n-input
            type="textarea"
            v-model:value="inputJson"
            placeholder='输入对象数组 (JSON 格式，例如: [{"key":1},{"key":2}])'
            :rows="5"
          />
          <n-input
            v-model:value="propertyKey"
            placeholder="要提取的属性名"
          />
        </div>
        <div class="switch-container">
          <span>是否排除空值</span>
          <n-switch v-model:value="excludeNil"/>
        </div>
        <n-button type="primary" @click="extractKeys">提取属性</n-button>
        <n-gradient-text type="info">{{ resultText }}</n-gradient-text>
      </n-space>
    </n-card>
  </div>
</template>

<style scoped>
textarea {
  width: 100%;
  height: 100px;
}
.input-container {
  display: flex;
  gap: 10px; /* 控制输入框之间的间距 */
}
.switch-container {
  display: flex;
  align-items: center;
  margin-bottom: 10px;
}

.switch-container span {
  margin-right: 5px;
  margin-left: 20px;
}
</style>
