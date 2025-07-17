<!-- <script setup>
import describe from './describe.vue'
import tags from './tags.vue'
</script> -->

<!-- <ClientOnly>
  <describe />
  <wordcloud/>
</ClientOnly> -->

<!-- ## 🏷️ 标签

<tags :className="'type-it1'" :values="['支持Vue3']" />
<tags :className="'type-it2'" :tagNameList="['浏览器']" :values="['支持任意运行在浏览器的JS语言']" :speed="100" />
<tags :className="'type-it3'" :tagNameList="['Node']" :values="['支持NodeJs']" /> -->

### 📦 安装

::: code-group

```bash [pnpm]
pnpm add buzzts
```

```bash [yarn]
yarn add buzzts
```

```bash [npm]
npm install buzzts
```

:::

### 📡 `CDN`

::: code-group

```html [jsdelivr]
<script src="//cdn.jsdelivr.net/npm/buzzts"></script>
```

```html [unpkg]
<script src="//unpkg.com/buzzts"></script>
```
:::

::: code-group

```js
// 使用 fetch 动态引入 buzzts 库
fetch('https://cdn.jsdelivr.net/npm/buzzts@latest')
    .then(response => response.text())
    .then(scriptText => {
        const script = document.createElement('script');
        script.textContent = scriptText;
        document.head.appendChild(script);

        // 确保 buzzts 已加载并且 randColorHEX 可用
        if (typeof buzzts.randColorHEX === 'function') {
            console.log('随机颜色:', buzzts.randColorHEX());
        } else {
            console.error('randColorHEX 函数未定义');
        }
    })
    .catch(error => console.error('加载脚本失败:', error));
```

```html
<!DOCTYPE html>
<html lang="zh">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>引入 buzzts 示例</title>
</head>
<body>
    <h1>欢迎使用 buzzts</h1>

    <!-- 引入 buzzts 库 -->
    <script src="https://cdn.jsdelivr.net/npm/buzzts@latest"></script>

    <script>
        // 等待文档加载完成
        window.onload = function() {
            // 确保 buzzts 已加载并且 randColorHEX 可用
            if (typeof buzzts.randColorHEX === 'function') {
                console.log('随机颜色:', buzzts.randColorHEX());
            } else {
                console.error('randColorHEX 函数未定义');
            }
        };
    </script>
</body>
</html>
```
:::

### 🤔 常见问题、反馈

问题：如果自己项目中的函数与 `buzzts` 内部的函数名称冲突怎么办？  
答：这种问题很常见，可以使用 `ES6` 提供的 `as` 关键字来为导入的函数重命名，如下：

```ts
import { deepClone as _deepClone } from "buzzts";
_deepClone(xxx);
```

[反馈问题、新增需求](https://github.com/kamalyes/buzzts-docs/issues/new)

### 🔔 温馨提示

本站大部分图片使用`Github`静态资源。如遇加载空白或加载图片失败时，刷新几次即可
