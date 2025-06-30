<script setup lang="ts">
import { ref, computed, watch, onMounted } from "vue";
import { StorageWrapper, StorageType } from "buzzts";

const localStorageWrapper = new StorageWrapper(StorageType.Local);

type DemoItem = { label: string; key: string; rawValue: any; value: string };

const demos: DemoItem[] = [
  { label: "字符串示例", key: "localKey1", rawValue: "localValue1", value: 'localValue1' },
  { label: "数字示例", key: "localKey2", rawValue: 12345, value: "12345" },
  { label: "布尔值示例", key: "localKey3", rawValue: true, value: "true" },
  { label: "对象示例", key: "localKey4", rawValue: { a: 1, b: "test" }, value: '{"a":1,"b":"test"}' },
  { label: "数组示例", key: "localKey5", rawValue: [1, 2, 3], value: "[1,2,3]" },
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
  // JSON.stringify rawVal，方便展示调用参数
  argsStr.value = `"${key.value}", ${JSON.stringify(rawVal.value)}`;

  try {
    // 存储时统一用 JSON.stringify
    localStorageWrapper.set(key.value, JSON.stringify(rawVal.value));
    result.value = `localStorage 设置成功: key=${key.value}, value=${JSON.stringify(rawVal.value)}`;
  } catch (e) {
    result.value = `设置失败: ${(e as Error).message}`;
  }
}

function getItem() {
  func.value = "get";
  argsStr.value = `"${key.value}"`;

  try {
    const v = localStorageWrapper.get(key.value);
    if (v === null) {
      result.value = "无对应值";
      return;
    }
    // 尝试 JSON.parse 还原原始类型
    try {
      const parsed = JSON.parse(v);
      result.value = `localStorage 读取到: ${JSON.stringify(parsed)}`;
    } catch {
      // 解析失败，直接显示字符串
      result.value = `localStorage 读取到: ${v}`;
    }
  } catch (e) {
    result.value = `读取失败: ${(e as Error).message}`;
  }
}

function removeItem() {
  func.value = "remove";
  argsStr.value = `"${key.value}"`;

  try {
    localStorageWrapper.remove(key.value);
    result.value = `localStorage 删除 key=${key.value} 成功`;
  } catch (e) {
    result.value = `删除失败: ${(e as Error).message}`;
  }
}

function clearStorage() {
  func.value = "clear";
  argsStr.value = "";

  try {
    localStorageWrapper.clear();
    result.value = "localStorage 已清空所有数据";
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
  // 当 rawVal 改变时，同步更新 val 的字符串表示，方便展示
  val.value = JSON.stringify(newVal);
});

onMounted(() => {
  selectDemo(0);
});

const resultText = computed(() => {
  if (!func.value) return "请点击操作按钮";
  return `localStorageWrapper.${func.value}(${argsStr.value})`;
});
</script>

<template>
  <n-card title="localStorage 操作演示 - 多数据类型支持">
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
        <!-- 这里用 textarea 方便编辑复杂 JSON -->
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
      <n-gradient-text type="info" v-if="resultText"> {{ resultText }} </n-gradient-text>
      <n-text style="white-space: pre-wrap; margin-top: 12px;" v-if="result">{{ result }}</n-text>
    </n-space>
  </n-card>
</template>
