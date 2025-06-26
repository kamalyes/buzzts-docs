<script setup>
import { useAddNumInOutlineLabel } from '../../.vitepress/utils/createElement.ts'
useAddNumInOutlineLabel(9)

import capitalizeFirstLetter from "./capitalizeFirstLetter.vue"
import camelToSnake from "./camelToSnake.vue"
import snakeToCamel from "./snakeToCamel.vue"
import toConstantCase from "./toConstantCase.vue"
import camelToSpace from "./camelToSpace.vue"
import maskPhoneNumber from "./maskPhoneNumber.vue"
import truncateText from "./truncateText.vue"
import escapeHtml from "./escapeHtml.vue"
import unescapeHtml from "./unescapeHtml.vue"

</script>

::: tip 支持任意 `JavaScript` 环境或框架
处理数组
:::

### capitalizeFirstLetter

将字符串首字母大写

<div class="buzzts-border">

#### <divider-base /> {#base-capitalizeFirstLetter}

<capitalizeFirstLetter />

<details>
<summary>查看代码</summary>

<<< @/utils/string/capitalizeFirstLetter.vue

</details>

#### <divider-param /> {#param-capitalizeFirstLetter}

| 参数属性 | 说明     | 类型   | 默认值 |
|----------|----------|--------|--------|
| input    | 输入字符串 | string | 无     |

| 返回值   | 说明                 |
|----------|----------------------|
| `string` | 首字母大写的字符串   |

#### <divider-desc /> {#desc-capitalizeFirstLetter}

- 将字符串首字母转换成大写
- 非字符串或空字符串原样返回

</div>

### camelToSnake

驼峰命名转蛇形命名

<div class="buzzts-border">

#### <divider-base /> {#base-camelToSnake}

<camelToSnake />

<details>
<summary>查看代码</summary>

<<< @/utils/string/camelToSnake.vue

</details>

#### <divider-param /> {#param-camelToSnake}

| 参数属性           | 说明                     | 类型                    | 默认值  |
|--------------------|--------------------------|-------------------------|---------|
| camelCaseStr       | 驼峰命名字符串             | string                  | 无      |
| options            | 配置选项                 | object                  | {}      |
| options.keepUnderscorePrefix | 是否保留前导下划线 | boolean                 | false   |

| 返回值   | 说明             |
|----------|------------------|
| `string` | 蛇形命名字符串   |

#### <divider-desc /> {#desc-camelToSnake}

- 将驼峰命名字符串转换为蛇形命名
- 支持保留前导下划线（默认不保留）
- 处理连续大写字母情况

</div>

### snakeToCamel

蛇形命名转驼峰命名

<div class="buzzts-border">

#### <divider-base /> {#base-snakeToCamel}

<snakeToCamel />

<details>
<summary>查看代码</summary>

<<< @/utils/string/snakeToCamel.vue

</details>

#### <divider-param /> {#param-snakeToCamel}

| 参数属性           | 说明                 | 类型                    | 默认值  |
|--------------------|----------------------|-------------------------|---------|
| snakeCaseStr       | 蛇形命名字符串         | string                  | 无      |
| options            | 配置选项             | object                  | {}      |
| options.pascalCase | 是否转换为帕斯卡命名   | boolean                 | false   |

| 返回值   | 说明             |
|----------|------------------|
| `string` | 驼峰命名字符串   |

#### <divider-desc /> {#desc-snakeToCamel}

- 将蛇形命名字符串转换为驼峰命名
- 支持转换为帕斯卡命名（首字母大写）

</div>

### toConstantCase

转换为常量命名（全大写下划线）

<div class="buzzts-border">

#### <divider-base /> {#base-toConstantCase}

<toConstantCase />

<details>
<summary>查看代码</summary>

<<< @/utils/string/toConstantCase.vue

</details>

#### <divider-param /> {#param-toConstantCase}

| 参数属性           | 说明                 | 类型                    | 默认值  |
|--------------------|----------------------|-------------------------|---------|
| str                | 输入字符串            | string \| null          | 无      |
| options            | 配置选项             | object                  | {}      |
| options.preserveNull | 输入非字符串时是否返回原值 | boolean           | false   |

| 返回值   | 说明             |
|----------|------------------|
| `string \| null` | 常量命名字符串或原值 |

#### <divider-desc /> {#desc-toConstantCase}

- 将字符串转换为全大写下划线格式
- 支持保留原值（非字符串）可选配置
- 已是常量格式时直接返回

</div>

### camelToSpace

驼峰命名转空格命名

<div class="buzzts-border">

#### <divider-base /> {#base-camelToSpace}

<camelToSpace />

<details>
<summary>查看代码</summary>

<<< @/utils/string/camelToSpace.vue

</details>

#### <divider-param /> {#param-camelToSpace}

| 参数属性           | 说明                 | 类型                    | 默认值  |
|--------------------|----------------------|-------------------------|---------|
| camelCaseStr       | 驼峰命名字符串         | string                  | 无      |
| options            | 配置选项             | object                  | {}      |
| options.capitalize | 是否首字母大写         | boolean                 | false   |

| 返回值   | 说明             |
|----------|------------------|
| `string` | 空格分隔字符串   |

#### <divider-desc /> {#desc-camelToSpace}

- 将驼峰命名转换为空格分隔的小写字符串
- 支持首字母大写选项

</div>

### maskPhoneNumber

加密手机号中间部分

<div class="buzzts-border">

#### <divider-base /> {#base-maskPhoneNumber}

<maskPhoneNumber />

<details>
<summary>查看代码</summary>

<<< @/utils/string/maskPhoneNumber.vue

</details>

#### <divider-param /> {#param-maskPhoneNumber}

| 参数属性           | 说明                 | 类型                    | 默认值  |
|--------------------|----------------------|-------------------------|---------|
| phoneNumber        | 手机号码（字符串或数字） | string \| number        | 无      |
| options            | 配置选项             | object                  | {}      |
| options.maskChar   | 替换字符             | string                  | '*'     |
| options.maskLength | 替换长度             | number                  | 4       |

| 返回值   | 说明             |
|----------|------------------|
| `string` | 加密后的手机号   |

#### <divider-desc /> {#desc-maskPhoneNumber}

- 支持字符串或数字手机号输入
- 默认替换中间4位为`*`
- 支持自定义替换字符和长度
- 非合法手机号格式会打印警告并原样返回

</div>

### truncateText

智能截断字符串

<div class="buzzts-border">

#### <divider-base /> {#base-truncateText}

<truncateText />

<details>
<summary>查看代码</summary>

<<< @/utils/string/truncateText.vue

</details>

#### <divider-param /> {#param-truncateText}

| 参数属性           | 说明                 | 类型                    | 默认值  |
|--------------------|----------------------|-------------------------|---------|
| text               | 原始文本             | string                  | 无      |
| maxLength          | 最大长度             | number                  | 无      |
| options            | 配置选项             | object                  | {}      |
| options.ellipsis   | 省略符号             | string                  | '...'   |
| options.keepWords  | 是否保持单词完整     | boolean                 | true    |

| 返回值   | 说明             |
|----------|------------------|
| `string` | 截断后的字符串   |

#### <divider-desc /> {#desc-truncateText}

- 超出长度时智能截断
- 支持保持单词完整或直接截断
- 支持自定义省略符号

</div>

### escapeHtml

HTML特殊字符转义

<div class="buzzts-border">

#### <divider-base /> {#base-escapeHtml}

<escapeHtml />

<details>
<summary>查看代码</summary>

<<< @/utils/string/escapeHtml.vue

</details>

#### <divider-param /> {#param-escapeHtml}

| 参数属性           | 说明                 | 类型                    | 默认值  |
|--------------------|----------------------|-------------------------|---------|
| htmlStr            | 包含HTML的字符串      | string                  | 无      |

| 返回值   | 说明             |
|----------|------------------|
| `string` | 转义后的安全字符串 |

#### <divider-desc /> {#desc-escapeHtml}

- 将 HTML 特殊字符转换为对应的实体编码
- 保障字符串安全防止XSS等攻击

</div>

### unescapeHtml

HTML实体反转义

<div class="buzzts-border">

#### <divider-base /> {#base-unescapeHtml}

<unescapeHtml />

<details>
<summary>查看代码</summary>

<<< @/utils/string/unescapeHtml.vue

</details>

#### <divider-param /> {#param-unescapeHtml}

| 参数属性           | 说明                 | 类型                    | 默认值  |
|--------------------|----------------------|-------------------------|---------|
| escapedStr         | 转义后的字符串        | string                  | 无      |

| 返回值   | 说明             |
|----------|------------------|
| `string` | 原始字符串       |

#### <divider-desc /> {#desc-unescapeHtml}

- 将 HTML 实体编码转换回对应字符
- 反转义常见实体，恢复原始字符串

</div>
