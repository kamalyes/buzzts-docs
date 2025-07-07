<script setup lang="ts">
import { ref, computed } from 'vue';
import { arrayToObject } from 'buzzts'

const inputArray = ref<string[]>(['item1', 'item2', null]);
const propertyKey = ref<string>('key');
const excludeNil = ref<boolean>(false);
const convertedObjects = ref<{ [key: string]: string }[]>([]);

const convertArrayToObject = () => {
  convertedObjects.value = arrayToObject(inputArray.value, propertyKey.value, excludeNil.value);
};

const resultText = computed(() => {
  if (convertedObjects.value.length < 1) return "点击转换数组";
  return `arrayToObject(${JSON.stringify(inputArray.value)}, '${propertyKey.value}', ${excludeNil.value}) = ${JSON.stringify(convertedObjects.value)}`;
});

</script>

<template>
  <div>
    <n-card title="数组转换为对象示例">
      <n-space vertical>
        <div class="input-container">
          <n-input
            type="textarea"
            v-model:value="inputArray"
            placeholder="输入字符串数组 (JSON 格式，例如: ['item1', 'item2', null])"
            :rows="5"
          />
          <n-input
            v-model:value="propertyKey"
            placeholder="要设置的属性名"
          />
        </div>
        <div class="switch-container">
          <span>是否排除空值</span>
          <n-switch v-model:value="excludeNil"/>
        </div>
        <n-button type="primary" @click="convertArrayToObject">转换数组</n-button>
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
