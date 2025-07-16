<script setup>
import { useAddNumInOutlineLabel } from '../../.vitepress/utils/createElement.ts'
useAddNumInOutlineLabel(32)

import copyToClipboard from './copyToClipboard.vue';
import getFromClipboard from './getFromClipboard.vue';
import removeHTMLTag from './removeHTMLTag.vue';
import escapeHTML from './escapeHTML.vue';
import setElementStyle from './setElementStyle.vue';
import getElementStyle from './getElementStyle.vue';
import setElementProperties from './setElementProperties.vue';
import toggleElementClass from './toggleElementClass.vue';
import hasElementClass from './hasElementClass.vue';
import addElementClass from './addElementClass.vue';
import removeElementClass from './removeElementClass.vue';
import getElementData from './getElementData.vue';
import setElementData from './setElementData.vue';
import removeElementData from './removeElementData.vue';
import createElement from './createElement.vue';
import appendElementChildren from './appendElementChildren.vue';
import delegateElementEvent from './delegateElementEvent.vue';
import serializeFormElement from './serializeFormElement.vue';
import setFormElementValues from './setFormElementValues.vue';
import isElementInViewport from './isElementInViewport.vue';
import animateTo from './animateTo.vue';
import getElementRect from './getElementRect.vue';
import smoothScrollTo from './smoothScrollTo.vue';
import getElementAttributes from './getElementAttributes.vue';
import setElementAttributes from './setElementAttributes.vue';
import removeElementAttributes from './removeElementAttributes.vue';
import getElementPosition from './getElementPosition.vue';
import getElementOffset from './getElementOffset.vue';
import getElementSize from './getElementSize.vue';
import hideElement from './hideElement.vue';
import showElement from './showElement.vue';
import isElementVisible from './isElementVisible.vue';

</script>

::: tip 支持任意 `JavaScript` 环境或框架
处理dom工具集
:::

### getFromClipboard

安全获取剪贴板文本内容

<div class="buzzts-border">

#### <divider-base /> {#base-getFromClipboard}

<getFromClipboard />

<details>
<summary>查看代码</summary>

<<< @/utils/dom/getFromClipboard.vue

</details>

#### <divider-param /> {#param-getFromClipboard}

| 参数属性 | 说明                          | 类型     | 默认值 |
|----------|-------------------------------|----------|--------|
| 无       | 无                            | -        | -      |

| 返回值   | 说明                                   |
|----------|----------------------------------------|
| `Promise<string>` | resolve时返回剪贴板文本，reject时返回错误 |

#### <divider-desc /> {#desc-getFromClipboard}

- 安全地读取剪贴板中的文本内容。

</div>

### copyToClipboard

安全写入文本到剪贴板

<div class="buzzts-border">

#### <divider-base /> {#base-copyToClipboard}

<copyToClipboard />

<details>
<summary>查看代码</summary>

<<< @/utils/dom/copyToClipboard.vue

</details>

#### <divider-param /> {#param-copyToClipboard}

| 参数属性 | 说明                          | 类型     | 默认值 |
|----------|-------------------------------|----------|--------|
| text     | 要写入的文本                  | `string` | -      |

| 返回值   | 说明                                   |
|----------|----------------------------------------|
| `Promise<void>` | 返回一个Promise，表示操作的结果 |

#### <divider-desc /> {#desc-copyToClipboard}

- 安全地将文本写入剪贴板。

</div>

### removeHTMLTag

移除字符串中的所有HTML标签，保留纯文本

<div class="buzzts-border">

#### <divider-base /> {#base-removeHTMLTag}

<removeHTMLTag />

<details>
<summary>查看代码</summary>

<<< @/utils/dom/removeHTMLTag.vue

</details>

#### <divider-param /> {#param-removeHTMLTag}

| 参数属性 | 说明                          | 类型     | 默认值 |
|----------|-------------------------------|----------|--------|
| str      | 包含HTML的字符串              | `string` | -      |

| 返回值   | 说明                                   |
|----------|----------------------------------------|
| `string` | 清理后的纯文本                        |

#### <divider-desc /> {#desc-removeHTMLTag}

- 从字符串中移除所有HTML标签。

</div>

### escapeHTML

转义HTML特殊字符，防止XSS攻击

<div class="buzzts-border">

#### <divider-base /> {#base-escapeHTML}

<escapeHTML />

<details>
<summary>查看代码</summary>

<<< @/utils/dom/escapeHTML.vue

</details>

#### <divider-param /> {#param-escapeHTML}

| 参数属性 | 说明                          | 类型     | 默认值 |
|----------|-------------------------------|----------|--------|
| str      | 需要转义的字符串              | `string` | -      |

| 返回值   | 说明                                   |
|----------|----------------------------------------|
| `string` | 转义后的安全字符串                    |

#### <divider-desc /> {#desc-escapeHTML}

- 转义字符串中的HTML特殊字符。

</div>

### setElementStyle

批量设置元素的内联样式

<div class="buzzts-border">

#### <divider-base /> {#base-setElementStyle}

<setElementStyle />

<details>
<summary>查看代码</summary>

<<< @/utils/dom/setElementStyle.vue

</details>

#### <divider-param /> {#param-setElementStyle}

| 参数属性 | 说明                          | 类型     | 默认值 |
|----------|-------------------------------|----------|--------|
| el       | 目标元素                      | `HTMLElement | null` | -      |
| styleObj | 样式键值对                    | `CSSStyleProps` | -      |

| 返回值   | 说明                                   |
|----------|----------------------------------------|
| `void`   | 无返回值                               |

#### <divider-desc /> {#desc-setElementStyle}

- 批量设置指定元素的内联样式。

</div>

### getElementStyle

获取元素的计算样式值

<div class="buzzts-border">

#### <divider-base /> {#base-getElementStyle}

<getElementStyle />

<details>
<summary>查看代码</summary>

<<< @/utils/dom/getElementStyle.vue

</details>

#### <divider-param /> {#param-getElementStyle}

| 参数属性 | 说明                          | 类型     | 默认值 |
|----------|-------------------------------|----------|--------|
| el       | 目标元素                      | `HTMLElement` | -      |
| property | 要获取的CSS属性名            | `string` | -      |

| 返回值   | 说明                                   |
|----------|----------------------------------------|
| `string` | 计算后的样式值                        |

#### <divider-desc /> {#desc-getElementStyle}

- 获取指定元素的计算样式值。

</div>

### setElementProperties

批量设置CSS自定义属性

<div class="buzzts-border">

#### <divider-base /> {#base-setElementProperties}

<setElementProperties />

<details>
<summary>查看代码</summary>

<<< @/utils/dom/setElementProperties.vue

</details>

#### <divider-param /> {#param-setElementProperties}

| 参数属性 | 说明                          | 类型     | 默认值 |
|----------|-------------------------------|----------|--------|
| el       | 目标元素                      | `HTMLElement | null` | -      |
| properties | 属性键值对                  | `Record<string, string | null>` | -      |

| 返回值   | 说明                                   |
|----------|----------------------------------------|
| `void`   | 无返回值                               |

#### <divider-desc /> {#desc-setElementProperties}

- 批量设置指定元素的CSS自定义属性。

</div>

### toggleElementClass

切换元素的类名

<div class="buzzts-border">

#### <divider-base /> {#base-toggleElementClass}

<toggleElementClass />

<details>
<summary>查看代码</summary>

<<< @/utils/dom/toggleElementClass.vue

</details>

#### <divider-param /> {#param-toggleElementClass}

| 参数属性 | 说明                          | 类型     | 默认值 |
|----------|-------------------------------|----------|--------|
| ele      | 目标元素                      | `HTMLElement` | -      |
| className | 要切换的类名                | `string` | -      |
| force    | 强制添加或移除                | `boolean` | -      |

| 返回值   | 说明                                   |
|----------|----------------------------------------|
| `boolean` | 操作后类名是否存在                    |

#### <divider-desc /> {#desc-toggleElementClass}

- 切换指定元素的类名。

</div>

### hasElementClass

检查元素是否包含指定类名

<div class="buzzts-border">

#### <divider-base /> {#base-hasElementClass}

<hasElementClass />

<details>
<summary>查看代码</summary>

<<< @/utils/dom/hasElementClass.vue

</details>

#### <divider-param /> {#param-hasElementClass}

| 参数属性 | 说明                          | 类型     | 默认值 |
|----------|-------------------------------|----------|--------|
| ele      | 目标元素                      | `HTMLElement` | -      |
| className | 要检查的类名                | `string` | -      |

| 返回值   | 说明                                   |
|----------|----------------------------------------|
| `boolean` | 是否包含该类名                        |

#### <divider-desc /> {#desc-hasElementClass}

- 检查指定元素是否包含特定的类名。

</div>

### addElementClass

为元素添加一个或多个类名

<div class="buzzts-border">

#### <divider-base /> {#base-addElementClass}

<addElementClass />

<details>
<summary>查看代码</summary>

<<< @/utils/dom/addElementClass.vue

</details>

#### <divider-param /> {#param-addElementClass}

| 参数属性 | 说明                          | 类型     | 默认值 |
|----------|-------------------------------|----------|--------|
| ele      | 目标元素                      | `HTMLElement` | -      |
| className | 要添加的类名（单个或多个）  | `string | string[]` | -      |

| 返回值   | 说明                                   |
|----------|----------------------------------------|
| `void`   | 无返回值                               |

#### <divider-desc /> {#desc-addElementClass}

- 为指定元素添加一个或多个类名。

</div>

### removeElementClass

从元素移除一个或多个类名

<div class="buzzts-border">

#### <divider-base /> {#base-removeElementClass}

<removeElementClass />

<details>
<summary>查看代码</summary>

<<< @/utils/dom/removeElementClass.vue

</details>

#### <divider-param /> {#param-removeElementClass}

| 参数属性 | 说明                          | 类型     | 默认值 |
|----------|-------------------------------|----------|--------|
| ele      | 目标元素                      | `HTMLElement` | -      |
| className | 要移除的类名（单个或多个）  | `string | string[]` | -      |

| 返回值   | 说明                                   |
|----------|----------------------------------------|
| `void`   | 无返回值                               |

#### <divider-desc /> {#desc-removeElementClass}

- 从指定元素移除一个或多个类名。

</div>

### getElementData

获取元素的自定义data属性值

<div class="buzzts-border">

#### <divider-base /> {#base-getElementData}

<getElementData />

<details>
<summary>查看代码</summary>

<<< @/utils/dom/getElementData.vue

</details>

#### <divider-param /> {#param-getElementData}

| 参数属性 | 说明                          | 类型     | 默认值 |
|----------|-------------------------------|----------|--------|
| ele      | 目标元素                      | `HTMLElement` | -      |
| key      | 属性名（不带data-前缀）      | `string` | -      |

| 返回值   | 说明                                   |
|----------|----------------------------------------|
| `string | null` | 属性值，不存在时返回null           |

#### <divider-desc /> {#desc-getElementData}

- 获取指定元素的自定义data属性值。

</div>

### setElementData

设置元素的自定义data属性

<div class="buzzts-border">

#### <divider-base /> {#base-setElementData}

<setElementData />

<details>
<summary>查看代码</summary>

<<< @/utils/dom/setElementData.vue

</details>

#### <divider-param /> {#param-setElementData}

| 参数属性 | 说明                          | 类型     | 默认值 |
|----------|-------------------------------|----------|--------|
| ele      | 目标元素                      | `HTMLElement` | -      |
| key      | 属性名（不带data-前缀）      | `string` | -      |
| value    | 要设置的值                    | `string` | -      |

| 返回值   | 说明                                   |
|----------|----------------------------------------|
| `void`   | 无返回值                               |

#### <divider-desc /> {#desc-setElementData}

- 设置指定元素的自定义data属性。

</div>

### removeElementData

移除元素的自定义data属性

<div class="buzzts-border">

#### <divider-base /> {#base-removeElementData}

<removeElementData />

<details>
<summary>查看代码</summary>

<<< @/utils/dom/removeElementData.vue

</details>

#### <divider-param /> {#param-removeElementData}

| 参数属性 | 说明                          | 类型     | 默认值 |
|----------|-------------------------------|----------|--------|
| ele      | 目标元素                      | `HTMLElement` | -      |
| key      | 属性名（不带data-前缀）      | `string` | -      |

| 返回值   | 说明                                   |
|----------|----------------------------------------|
| `void`   | 无返回值                               |

#### <divider-desc /> {#desc-removeElementData}

- 移除指定元素的自定义data属性。

</div>

### getElementAttributes

获取元素的所有属性

<div class="buzzts-border">

#### <divider-base /> {#base-getElementAttributes}

<getElementAttributes />

<details>
<summary>查看代码</summary>

<<< @/utils/dom/getElementAttributes.vue

</details>

#### <divider-param /> {#param-getElementAttributes}

| 参数属性 | 说明                          | 类型     | 默认值 |
|----------|-------------------------------|----------|--------|
| el       | 目标元素                      | `HTMLElement` | -      |

| 返回值   | 说明                                   |
|----------|----------------------------------------|
| `Record<string, string>` | 元素的所有属性键值对 |

#### <divider-desc /> {#desc-getElementAttributes}

- 获取指定元素的所有属性及其值。

</div>

### setElementAttributes

设置元素的多个属性

<div class="buzzts-border">

#### <divider-base /> {#base-setElementAttributes}

<setElementAttributes />

<details>
<summary>查看代码</summary>

<<< @/utils/dom/setElementAttributes.vue

</details>

#### <divider-param /> {#param-setElementAttributes}

| 参数属性 | 说明                          | 类型     | 默认值 |
|----------|-------------------------------|----------|--------|
| el       | 目标元素                      | `HTMLElement` | -      |
| attrs    | 属性键值对                    | `Record<string, string>` | -      |

| 返回值   | 说明                                   |
|----------|----------------------------------------|
| `void`   | 无返回值                               |

#### <divider-desc /> {#desc-setElementAttributes}

- 批量设置指定元素的多个属性。

</div>

### removeElementAttributes

移除元素的多个属性

<div class="buzzts-border">

#### <divider-base /> {#base-removeElementAttributes}

<removeElementAttributes />

<details>
<summary>查看代码</summary>

<<< @/utils/dom/removeElementAttributes.vue

</details>

#### <divider-param /> {#param-removeElementAttributes}

| 参数属性 | 说明                          | 类型     | 默认值 |
|----------|-------------------------------|----------|--------|
| el       | 目标元素                      | `HTMLElement` | -      |
| attrs    | 要移除的属性名数组            | `string[]` | -      |

| 返回值   | 说明                                   |
|----------|----------------------------------------|
| `void`   | 无返回值                               |

#### <divider-desc /> {#desc-removeElementAttributes}

- 移除指定元素的多个属性。

</div>

### createElement

创建一个新的DOM元素

<div class="buzzts-border">

#### <divider-base /> {#base-createElement}

<createElement />

<details>
<summary>查看代码</summary>

<<< @/utils/dom/createElement.vue

</details>

#### <divider-param /> {#param-createElement}

| 参数属性 | 说明                          | 类型     | 默认值 |
|----------|-------------------------------|----------|--------|
| tagName  | 要创建的元素标签名            | `string` | -      |
| props    | 元素的属性                    | `Record<string, string>` | -      |

| 返回值   | 说明                                   |
|----------|----------------------------------------|
| `HTMLElement` | 创建的新元素对象                  |

#### <divider-desc /> {#desc-createElement}

- 创建一个新的DOM元素，并可以设置其属性。

</div>

### getElementPosition

获取元素的相对位置

<div class="buzzts-border">

#### <divider-base /> {#base-getElementPosition}

<getElementPosition />

<details>
<summary>查看代码</summary>

<<< @/utils/dom/getElementPosition.vue

</details>

#### <divider-param /> {#param-getElementPosition}

| 参数属性 | 说明                          | 类型     | 默认值 |
|----------|-------------------------------|----------|--------|
| el       | 目标元素                      | `HTMLElement` | -      |

| 返回值   | 说明                                   |
|----------|----------------------------------------|
| `DOMRect` | 元素的位置信息                        |

#### <divider-desc /> {#desc-getElementPosition}

- 获取指定元素的相对位置信息。

</div>

### getElementOffset

获取元素的偏移量

<div class="buzzts-border">

#### <divider-base /> {#base-getElementOffset}

<getElementOffset />

<details>
<summary>查看代码</summary>

<<< @/utils/dom/getElementOffset.vue

</details>

#### <divider-param /> {#param-getElementOffset}

| 参数属性 | 说明                          | 类型     | 默认值 |
|----------|-------------------------------|----------|--------|
| el       | 目标元素                      | `HTMLElement` | -      |

| 返回值   | 说明                                   |
|----------|----------------------------------------|
| `{ top: number, left: number }` | 元素的偏移量信息 |

#### <divider-desc /> {#desc-getElementOffset}

- 获取指定元素的偏移量信息。

</div>

### getElementSize

获取元素的大小

<div class="buzzts-border">

#### <divider-base /> {#base-getElementSize}

<getElementSize />

<details>
<summary>查看代码</summary>

<<< @/utils/dom/getElementSize.vue

</details>

#### <divider-param /> {#param-getElementSize}

| 参数属性 | 说明                          | 类型     | 默认值 |
|----------|-------------------------------|----------|--------|
| el       | 目标元素                      | `HTMLElement` | -      |

| 返回值   | 说明                                   |
|----------|----------------------------------------|
| `{ width: number, height: number }` | 元素的宽高信息 |

#### <divider-desc /> {#desc-getElementSize}

- 获取指定元素的宽高信息。

</div>

### hideElement

隐藏指定元素

<div class="buzzts-border">

#### <divider-base /> {#base-hideElement}

<hideElement />

<details>
<summary>查看代码</summary>

<<< @/utils/dom/hideElement.vue

</details>

#### <divider-param /> {#param-hideElement}

| 参数属性 | 说明                          | 类型     | 默认值 |
|----------|-------------------------------|----------|--------|
| el       | 目标元素                      | `HTMLElement` | -      |

| 返回值   | 说明                                   |
|----------|----------------------------------------|
| `void`   | 无返回值                               |

#### <divider-desc /> {#desc-hideElement}

- 隐藏指定元素。

</div>

### showElement

显示指定元素

<div class="buzzts-border">

#### <divider-base /> {#base-showElement}

<showElement />

<details>
<summary>查看代码</summary>

<<< @/utils/dom/showElement.vue

</details>

#### <divider-param /> {#param-showElement}

| 参数属性 | 说明                          | 类型     | 默认值 |
|----------|-------------------------------|----------|--------|
| el       | 目标元素                      | `HTMLElement` | -      |

| 返回值   | 说明                                   |
|----------|----------------------------------------|
| `void`   | 无返回值                               |

#### <divider-desc /> {#desc-showElement}

- 显示指定元素。

</div>

### isElementVisible

检查元素是否可见

<div class="buzzts-border">

#### <divider-base /> {#base-isElementVisible}

<isElementVisible />

<details>
<summary>查看代码</summary>

<<< @/utils/dom/isElementVisible.vue

</details>

#### <divider-param /> {#param-isElementVisible}

| 参数属性 | 说明                          | 类型     | 默认值 |
|----------|-------------------------------|----------|--------|
| el       | 目标元素                      | `HTMLElement` | -      |

| 返回值   | 说明                                   |
|----------|----------------------------------------|
| `boolean` | 元素是否可见                        |

#### <divider-desc /> {#desc-isElementVisible}

- 检查指定元素是否可见。

</div>

### isElementInViewport

检查元素是否在视口内

<div class="buzzts-border">

#### <divider-base /> {#base-isElementInViewport}

<isElementInViewport />

<details>
<summary>查看代码</summary>

<<< @/utils/dom/isElementInViewport.vue

</details>

#### <divider-param /> {#param-isElementInViewport}

| 参数属性 | 说明                          | 类型     | 默认值 |
|----------|-------------------------------|----------|--------|
| el       | 目标元素                      | `HTMLElement` | -      |

| 返回值   | 说明                                   |
|----------|----------------------------------------|
| `boolean` | 元素是否在视口内                    |

#### <divider-desc /> {#desc-isElementInViewport}

- 检查指定元素是否在当前视口内。

</div>

### getElementRect

获取元素相对于文档的位置和尺寸

<div class="buzzts-border">

#### <divider-base /> {#base-getElementRect}

<getElementRect />

<details>
<summary>查看代码</summary>

<<< @/utils/dom/getElementRect.vue

</details>

#### <divider-desc /> {#desc-getElementRect}

- 获取指定元素相对于文档的位置和尺寸信息。

</div>

### smoothScrollTo

平滑滚动到指定位置或元素

<div class="buzzts-border">

#### <divider-base /> {#base-smoothScrollTo}

<smoothScrollTo />

<details>
<summary>查看代码</summary>

<<< @/utils/dom/smoothScrollTo.vue

</details>

#### <divider-desc /> {#desc-smoothScrollTo}

- 平滑滚动到指定元素或位置。

</div>