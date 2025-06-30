<script setup lang="ts">
import { ref, watch, onMounted, computed } from "vue";
import { StorageWrapper, StorageType } from "buzzts";

const sessionStorageWrapper = new StorageWrapper(StorageType.Session);

type DemoItem = { label: string; key: string; rawValue: any; value: string };

const demos: DemoItem[] = [
  { label: "字符串示例", key: "sessionKey1", rawValue: "sessionValue1", value: "sessionValue1" },
  { label: "数字示例", key: "sessionKey2", rawValue: 2023, value: "2023" },
  { label: "布尔值示例", key: "sessionKey3", rawValue: false, value: "false" },
  { label: "对象示例", key: "sessionKey4", rawValue: { name: "vue", version: 3 }, value: '{"name":"vue","version":3}' },
  { label: "数组示例", key: "sessionKey5", rawValue: [1, 2, 3, 4], value: "[1,2,3,4]" },
];

const selectedIndex = ref(0);
const key = ref(demos[0].key);
const val = ref(demos[0].value);
const rawVal = ref(demos[0].rawValue);
const result = ref("");

const func = ref("");
const argsStr = ref("");

function setItem() {
  func.value = "set";
  argsStr.value = `"${key.value}", ${JSON.stringify(rawVal.value)}`;

  try {
    sessionStorageWrapper.set(key.value, JSON.stringify(rawVal.value));
    result.value = `sessionStorage 设置成功: key=${key.value}, value=${JSON.stringify(rawVal.value)}`;
  } catch (e) {
    result.value = `设置失败: ${(e as Error).message}`;
  }
}

function getItem() {
  func.value = "get";
  argsStr.value = `"${key.value}"`;

  try {
    const v = sessionStorageWrapper.get(key.value);
    if (v === null) {
      result.value = "无对应值";
      return;
    }
    try {
      const parsed = JSON.parse(v);
      result.value = `sessionStorage 读取到: ${JSON.stringify(parsed)}`;
    } catch {
      result.value = `sessionStorage 读取到: ${v}`;
    }
  } catch (e) {
    result.value = `读取失败: ${(e as Error).message}`;
  }
}

function removeItem() {
  func.value = "remove";
  argsStr.value = `"${key.value}"`;

  try {
    sessionStorageWrapper.remove(key.value);
    result.value = `sessionStorage 删除 key=${key.value} 成功`;
  } catch (e) {
    result.value = `删除失败: ${(e as Error).message}`;
  }
}

function clearStorage() {
  func.value = "clear";
  argsStr.value = "";

  try {
    sessionStorageWrapper.clear();
    result.value = "sessionStorage 已清空所有数据";
  } catch (e) {
    result.value = `清空失败: ${(e as Error).message}`;
  }
}

function selectDemo(index: number) {
  selectedIndex.value = index;
  key.value = demos[index].key;
  rawVal.value = demos[index].rawValue;
  val.value = demos[index].value;
  result.value = "";
  func.value = "";
  argsStr.value = "";
}

watch(key, () => {
  result.value = "";
  func.value = "";
  argsStr.value = "";
});

watch(rawVal, (newVal) => {
  val.value = JSON.stringify(newVal);
});

onMounted(() => {
  selectDemo(0);
});
const resultText = computed(() => {
  if (!func.value) return "请点击操作按钮";
  return `sessionStorageWrapper.${func.value}(${argsStr.value})`;
});
</script>

<template>
  <n-card title="sessionStorage 操作演示 - 多数据类型支持">
    <n-space vertical size="large">
      <n-space wrap>
        <n-button
          v-for="(item, index) in demos"
          :key="index"
          size="small"
          :type="selectedIndex === index ? 'primary' : 'default'"
          @click="selectDemo(index)"
        >
          {{ item.label }}
        </n-button>
      </n-space>

      <n-space>
        <n-input v-model:value="key" placeholder="请输入 key" style="width: 200px" />
        <n-input
          v-model:value="val"
          placeholder="请输入 value (JSON 格式)"
          style="width: 300px"
          type="textarea"
          rows="3"
          @input="(e) => {
            try {
              rawVal.value = JSON.parse(e.target.value);
            } catch {
              rawVal.value = e.target.value;
            }
          }"
        />
      </n-space>

      <n-space>
        <n-button type="success" @click="setItem">设置</n-button>
        <n-button type="info" @click="getItem">读取</n-button>
        <n-button type="warning" @click="removeItem">删除</n-button>
        <n-button type="error" @click="clearStorage">清空全部</n-button>
      </n-space>

      <n-gradient-text type="info" v-if="resultText">{{ resultText }}</n-gradient-text>
      <n-text style="white-space: pre-wrap; margin-top: 12px;" v-if="result">{{ result }}</n-text>
    </n-space>
  </n-card>
</template>
