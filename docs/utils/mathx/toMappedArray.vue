<script setup lang="ts">
import { ref, computed } from 'vue';
import { toMappedArray } from 'buzzts';

const inputArray = ref<string>("[{\"value\":\"item\", \"label\":\"null\"}, {\"value\":\"item1\", \"label\":\"Item 1\"}, {\"value\":\"item2\", \"label\":\"Item 2\"}]"); // JSON 字符串格式
const inKeyField = ref<string>('value');
const inValueField = ref<string>('label');
const outKeyField = ref<string>('key');
const outValueField = ref<string>('value');
const includeKey = ref<boolean>(true);
const includeValue = ref<boolean>(true);
const excludeNil = ref<boolean>(false);
const convertedObjects = ref<{ [key: string]: string }[]>([]);
const isValidJson = ref<boolean>(true); // 用于跟踪输入的有效性

const goToMappedArray = () => {
  try {
    const parsedArray = JSON.parse(inputArray.value) as Array<{ [key: string]: any }>;
    const filteredArray = excludeNil.value ? parsedArray.filter(item => item !== null && item !== undefined) : parsedArray;
    convertedObjects.value = toMappedArray(filteredArray, {
      inKeyField: inKeyField.value,
      inValueField: inValueField.value,
      outKeyField: outKeyField.value,
      outValueField: outValueField.value,
      includeKey: includeKey.value,
      includeValue: includeValue.value
    });
  } catch (error) {
    convertedObjects.value = [];
    console.error("无效的输入格式:", error);
  }
};

const resultText = computed(() => {
  if (convertedObjects.value.length < 1) return "点击转换数组";
  return `toMappedArray(${inputArray.value}, '${inKeyField.value}', '${inValueField.value}', '${outKeyField.value}', '${outValueField.value}', ${includeKey.value}, ${includeValue.value}, ${excludeNil.value}) = ${JSON.stringify(convertedObjects.value)}`;
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
            placeholder='输入字符串数组 (JSON 格式，例如: [{"value":"item1", "label":"Item 1"}, {"value":"item2", "label":"Item 2"}])'
            :rows="3"
            @input="validateJson(inputArray)"
          />
          <div v-if="!isValidJson" style="color: red;">输入的 JSON 格式无效，请检查。</div>
        </div>
        <n-input
          v-model:value="inKeyField"
          placeholder="输入键字段名 (例如: 'value')"
        />
        <n-input
          v-model:value="inValueField"
          placeholder="输入值字段名 (例如: 'label')"
        />
        <n-input
          v-model:value="outKeyField"
          placeholder="输出键字段名 (例如: 'key')"
        />
        <n-input
          v-model:value="outValueField"
          placeholder="输出值字段名 (例如: 'value')"
        />
        <div class="switch-container">
          <span>包含键</span>
          <n-switch v-model:value="includeKey" />
          <span>包含值</span>
          <n-switch v-model:value="includeValue" />
          <span>是否排除空值</span>
          <n-switch v-model:value="excludeNil"/>
        </div>
        <n-button type="primary" @click="goToMappedArray">转换数组</n-button>
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
