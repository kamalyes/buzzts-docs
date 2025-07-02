<script setup>
import { useAddNumInOutlineLabel } from '../../.vitepress/utils/createElement.ts'
useAddNumInOutlineLabel(20)
import fullscreen from "./fullscreen.vue"
import scroller from "./scroller.vue"
import tagOpener from "./tagOpener.vue"
import isBrowser from "./isBrowser.vue"
import isSupportWebP from "./isSupportWebP.vue"
import viewport from "./viewport.vue"

</script>

::: tip 支持任意 `JavaScript` 环境或框架
浏览器操作工具集
:::

### Fullscreen

封装浏览器全屏操作，支持多浏览器兼容。

<div class="buzzts-border">

#### <divider-base /> {#base-Fullscreen}

<fullscreen />

<details>
<summary>查看代码</summary>

<<< @/utils/browser/fullscreen.vue

</details>

#### <divider-param /> {#param-Fullscreen}

| 参数属性 | 说明                                 | 类型        | 默认值        |
| -------- | ------------------------------------ | ----------- | ------------- |
| element  | 需要进入全屏的元素，默认是 body 元素 | HTMLElement | document.body |

| 返回值  | 说明                                                        |
| ------- | ----------------------------------------------------------- |
| enter() | 返回一个 Promise，成功时 resolve，失败时 reject（不支持时） |
| exit()  | 退出全屏，无返回值                                          |

#### <divider-desc /> {#desc-Fullscreen}

- 兼容多浏览器的全屏 API 封装
- 支持指定元素进入全屏，默认是 body 元素
- enter() 返回 Promise，方便链式调用和错误捕获
- exit() 立即退出全屏

</div>

### Scroller

平滑滚动控制类，支持横向和纵向的绝对及相对滚动，提供暂停、恢复和取消动画功能。

<div class="buzzts-border">

#### <divider-base /> {#base-Scroller}

<scroller />

<details>
<summary>查看代码</summary>

<<< @/utils/browser/scroller.vue

</details>

#### <divider-param /> {#param-Scroller}

| 参数属性 | 说明                 | 类型                         | 默认值          |
|----------|----------------------|------------------------------|-----------------|
| container| 滚动容器，HTMLElement 或 window | HTMLElement \| Window      | window          |

| 返回值   | 说明                   |
|----------|------------------------|
| `Scroller`实例 | 支持链式调用的滚动控制类实例 |

#### <divider-desc /> {#desc-Scroller}

- 支持纵向和横向滚动到指定绝对位置（`xTo` / `yTo`）  
- 支持横向和纵向相对滚动（`moveX` / `moveY`），滚动距离可正负  
- 支持自定义动画持续时间（单位：毫秒）和缓动函数（默认使用 `easeInOutQuad`）  
- 支持暂停（`pause`）、恢复（`resume`）和取消（`cancel`）动画  
- 通过动画帧逐步更新滚动位置，实现平滑滚动效果  
- 适合需要对滚动行为进行精细控制的场景，如滚动导航、滚动动画等  
- 提供链式调用，方便连续调用和组合操作  
- 提供 `isScrolling()` 方法判断当前是否处于滚动动画中（且未暂停）  

#### <divider-easing /> {#easing-Scroller}

默认缓动函数 `easeInOutQuad`：

```ts
const defaultEasing: EasingFunction = t => (t < 0.5 ? 2 * t * t : -1 + (4 - 2 * t) * t);
```

- 输入参数 `t` 是归一化时间进度，范围 `[0, 1]`  
- 返回值是缓动结果，范围 `[0, 1]`，用于计算滚动位置的插值  

#### <divider-usage /> {#usage-Scroller}

```ts
import { Scroller } from 'buzzts';

// 创建实例，默认滚动容器为 window
const scroller = new Scroller();

// 滚动到纵向绝对位置 300px，动画持续 600ms，使用默认缓动
scroller.yTo(300, { duration: 600 });

// 横向相对滚动 100px，使用自定义缓动函数
scroller.moveX(100, {
  easing: t => t * t, // 简单的加速缓动
});

// 暂停动画
scroller.pause();

// 恢复动画
scroller.resume();

// 取消当前动画
scroller.cancel();

// 判断是否正在滚动
if (scroller.isScrolling()) {
  console.log('正在滚动中');
}
```

</div>

### TagOpener

页面打开工具类，支持新标签页、弹窗及内嵌iframe三种打开方式

<div class="buzzts-border">

#### <divider-base /> {#base-TagOpener}

<tagOpener />

<details>
<summary>查看代码</summary>

<<< @/utils/browser/tagOpener.vue

</details>

#### <divider-param /> {#param-TagOpener}

| 参数属性      | 说明                                   | 类型                    | 默认值                        |
|---------------|--------------------------------------|-------------------------|-------------------------------|
| url           | 目标链接地址                         | string                  | 无                            |
| tagType       | 打开方式，默认新标签页。可选值见 `TagOpener.OpenType` | number                  | `TagOpener.OpenType.NEW_TAB`  |
| popupOptions  | 弹窗参数配置，仅 `POPUP` 方式生效    | {@link PopupOptions}     | 默认弹窗参数配置              |
| callbacks     | 打开页面相关回调函数                  | {@link OpenCallbacks}    | 无                            |
| embedContainer| 内嵌打开时的容器元素，仅 `EMBEDDED` 方式生效 | HTMLElement             | 无                            |

| 返回值 | 说明                         |
|--------|------------------------------|
| void   | 无返回值                     |

#### <divider-desc /> {#desc-TagOpener}

- 支持三种打开方式：
  - 新标签页（`NEW_TAB`）
  - 弹窗（`POPUP`），支持自定义窗口参数和弹窗关闭回调
  - 内嵌iframe（`EMBEDDED`），需要传入容器元素

- 弹窗参数配置详见 `PopupOptions` 接口说明

</div>

### isBrowser

检测代码是否运行在浏览器环境

<div class="buzzts-border">

#### <divider-base /> {#base-isBrowser}

<isBrowser />

<details>
<summary>查看代码</summary>

<<< @/utils/browser/isBrowser.vue

</details>

#### <divider-param /> {#param-isBrowser}

| 参数属性 | 说明 | 类型 | 默认值 |
|----------|------|------|--------|
| 无       | 无   | 无   | 无     |

| 返回值   | 说明           |
|----------|----------------|
| `boolean`| 是否为浏览器环境 |

#### <divider-desc /> {#desc-isBrowser}

- 通过检测 `window` 和 `document` 对象是否存在，判断当前代码是否运行于浏览器环境。

</div>

### isSupportWebP

判断浏览器是否支持 WebP 格式图片

<div class="buzzts-border">

#### <divider-base /> {#base-isSupportWebP}

<isSupportWebP />

<details>
<summary>查看代码</summary>

<<< @/utils/browser/isSupportWebP.vue

</details>

#### <divider-param /> {#param-isSupportWebP}

| 参数属性 | 说明 | 类型 | 默认值 |
|----------|------|------|--------|
| 无       | 无   | 无   | 无     |

| 返回值   | 说明                     |
|----------|--------------------------|
| `boolean`| 当前浏览器是否支持 WebP 图片格式 |

#### <divider-desc /> {#desc-isSupportWebP}

- 通过创建 canvas 元素并尝试生成 WebP 格式数据 URL，判断浏览器是否支持 WebP 图片格式。
- 在非浏览器环境（如 SSR）默认返回不支持。

</div>

### Viewport

兼容所有浏览器的视口尺寸工具类，提供宽高属性，支持监听窗口尺寸变化事件。

<div class="buzzts-border">

#### <divider-base /> {#base-Viewport}

<viewport />

<details>
<summary>查看代码</summary>

<<< @/utils/browser/viewport.vue

</details>

#### <divider-param /> {#param-Viewport}

| 参数属性 | 说明                         | 类型       | 默认值 |
|----------|------------------------------|------------|--------|
| 无       | 无                           | 无         | 无     |

| 返回值   | 说明                         |
|----------|------------------------------|
| 无       | 通过实例属性和方法访问视口信息 |

#### <divider-desc /> {#desc-Viewport}

- `width` 和 `height` 属性分别表示当前视口宽度和高度，单位为像素。
- `size()` 方法返回包含当前宽高的对象 `{ width, height }`。
- `refresh()` 方法手动刷新视口尺寸，重新计算宽高。
- `onResize(callback)` 方法监听窗口尺寸变化事件，自动刷新宽高并调用回调函数。
- `offResize()` 方法取消监听窗口尺寸变化事件，移除回调函数。
- 兼容所有主流浏览器，非浏览器环境宽高返回 0。

</div>
