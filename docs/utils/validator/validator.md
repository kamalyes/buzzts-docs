<script setup>
import { useAddNumInOutlineLabel } from '../../.vitepress/utils/createElement.ts'
useAddNumInOutlineLabel(34)
import isUndefined from "./isUndefined.vue"
import isNull from "./isNull.vue"
import isNil from "./isNil.vue"
import isBoolean from "./isBoolean.vue"
import isNumberWithRules from "./isNumberWithRules.vue"
import isString from "./isString.vue"
import isEmpty from "./isEmpty.vue"
import isIPv4 from "./isIPv4.vue"
import IsIPv6 from "./isIPv6.vue"
import isEmail from "./isEmail.vue"
import isFunction from "./isFunction.vue"
import isArray from "./isArray.vue"
import isObject from "./isObject.vue"
import isUrl from "./isUrl.vue"
import isSymbol from "./isSymbol.vue"
import isBigInt from "./isBigInt.vue"
import getTypeOf from "./getTypeOf.vue"
import isDataTime from "./isDataTime.vue"
import isPostCode from "./isPostCode.vue"
import isChineseIDCardNumber from "./isChineseIDCardNumber.vue"
import isHasEmoji from "./isHasEmoji.vue"
import isHexColor from "./isHexColor.vue"
import isTelNumber from "./isTelNumber.vue"
import isNLen from "./isNLen.vue"
import isEnCharacter from "./isEnCharacter.vue"
import isUpEnCharacter from "./isUpEnCharacter.vue"
import isLowerEnCharacter from "./isLowerEnCharacter.vue"
import isNumberEnCharacter from "./isNumberEnCharacter.vue"
import isNumberEnUnderscores from "./isNumberEnUnderscores.vue"
import isIsContainSpecialCharacter from "./isIsContainSpecialCharacter.vue"
import isEmptyLine from "./isEmptyLine.vue"
import isChines from "./isChines.vue"
import isDoubleByte from "./isDoubleByte.vue"
import isHex from "./isHex.vue"

</script>

::: tip 支持任意 `JavaScript` 环境或框架
处理数组
:::

### isUndefined

判断是否为 undefined

<div class="buzzts-border">

#### <divider-base /> {#base-isUndefined}

<isUndefined />

<details>
<summary>查看代码</summary>

<<< @/utils/validator/isUndefined.vue

</details>

#### <divider-param /> {#param-isUndefined}

| 参数属性 | 说明     | 类型 | 默认值 |
|----------|----------|------|--------|
| val      | 任意值   | any  | 无     |

| 返回值   | 说明            |
|----------|-----------------|
| boolean  | 是否为 undefined |

#### <divider-desc /> {#desc-isUndefined}

- 判断传入值是否严格等于 `undefined`

</div>

### isNull

判断是否为 null

<div class="buzzts-border">

#### <divider-base /> {#base-isNull}

<isNull />

<details>
<summary>查看代码</summary>

<<< @/utils/validator/isNull.vue

</details>

#### <divider-param /> {#param-isNull}

| 参数属性 | 说明     | 类型 | 默认值 |
|----------|----------|------|--------|
| val      | 任意值   | any  | 无     |

| 返回值   | 说明        |
|----------|-------------|
| boolean  | 是否为 null |

#### <divider-desc /> {#desc-isNull}

- 判断传入值是否严格等于 `null`

</div>

### isNil

判断是否为 null 或 undefined

<div class="buzzts-border">

#### <divider-base /> {#base-isNil}

<isNil />

<details>
<summary>查看代码</summary>

<<< @/utils/validator/isNil.vue

</details>

#### <divider-param /> {#param-isNil}

| 参数属性 | 说明     | 类型 | 默认值 |
|----------|----------|------|--------|
| val      | 任意值   | any  | 无     |

| 返回值   | 说明                |
|----------|---------------------|
| boolean  | 是否为 null 或 undefined |

#### <divider-desc /> {#desc-isNil}

- 判断传入值是否为 `null` 或 `undefined`

</div>

### isBoolean

判断是否为布尔值

<div class="buzzts-border">

#### <divider-base /> {#base-isBoolean}

<isBoolean />

<details>
<summary>查看代码</summary>

<<< @/utils/validator/isBoolean.vue

</details>

#### <divider-param /> {#param-isBoolean}

| 参数属性 | 说明     | 类型 | 默认值 |
|----------|----------|------|--------|
| val      | 任意值   | any  | 无     |

| 返回值   | 说明            |
|----------|-----------------|
| boolean  | 是否为布尔值    |

#### <divider-desc /> {#desc-isBoolean}

- 判断传入值类型是否为布尔值

</div>

### isNumberWithRules

校验字符串是否符合灵活配置的数字格式（支持符号、小数、整数长度等多种规则）

<div class="buzzts-border">

#### <divider-base /> {#base-isNumberWithRules}

<isNumberWithRules />

<details>
<summary>查看代码</summary>

<<< @/utils/validator/isNumberWithRules.vue

</details>

#### <divider-param /> {#param-isNumberWithRules}

| 参数属性            | 说明                                  | 类型       | 默认值 |
|---------------------|---------------------------------------|------------|--------|
| str                 | 待校验字符串                          | string     | 无     |
| options             | 配置项对象                            | object     | {}     |
| options.allowPositiveSign | 是否允许正号 '+'                | boolean    | true   |
| options.allowNegativeSign | 是否允许负号 '-'                | boolean    | true   |
| options.minIntegerLength   | 整数部分最小长度                | number     | 1      |
| options.maxIntegerLength   | 整数部分最大长度                | number     | 不限   |
| options.allowDecimal       | 是否允许小数                   | boolean    | false  |
| options.minDecimalLength   | 小数部分最小长度                | number     | 0      |
| options.maxDecimalLength   | 小数部分最大长度                | number     | 0      |
| options.allowNoIntegerPart | 是否允许无整数部分（如 `.15`） | boolean    | false  |
| options.nonZeroStart       | 整数部分是否必须非零开头        | boolean    | true   |

| 返回值              | 说明                                  |
|---------------------|---------------------------------------|
| `boolean`           | 是否符合配置规则的数字字符串            |

#### <divider-desc /> {#desc-isNumberWithRules}

- 支持正负号的灵活配置  
- 支持整数部分长度限制（最小和最大）  
- 支持是否允许整数以0开头  
- 支持小数部分长度限制（最小和最大）  
- 支持是否允许无整数部分的小数（如 `.45`）  
- 适用于多种复杂数字校验场景

</div>

### isString

判断是否为字符串

<div class="buzzts-border">

#### <divider-base /> {#base-isString}

<isString />

<details>
<summary>查看代码</summary>

<<< @/utils/validator/isString.vue

</details>

#### <divider-param /> {#param-isString}

| 参数属性 | 说明     | 类型 | 默认值 |
|----------|----------|------|--------|
| val      | 任意值   | any  | 无     |

| 返回值   | 说明            |
|----------|-----------------|
| boolean  | 是否为字符串    |

#### <divider-desc /> {#desc-isString}

- 判断传入值类型是否为字符串

</div>

### isEmpty

判断是否为空值（null、undefined、空字符串、空数组、空对象）

<div class="buzzts-border">

#### <divider-base /> {#base-isEmpty}

<isEmpty />

<details>
<summary>查看代码</summary>

<<< @/utils/validator/isEmpty.vue

</details>

#### <divider-param /> {#param-isEmpty}

| 参数属性 | 说明     | 类型 | 默认值 |
|----------|----------|------|--------|
| val      | 任意值   | any  | 无     |

| 返回值   | 说明            |
|----------|-----------------|
| boolean  | 是否为空值      |

#### <divider-desc /> {#desc-isEmpty}

- 判断传入值是否为 null、undefined、空字符串（含空白）、空数组或空对象（非内置对象）

</div>

### isEmptyLine

校验字符串是否为空行（仅空白字符）

<div class="buzzts-border">

#### <divider-base /> {#base-isEmptyLine}

<isEmptyLine />

<details>
<summary>查看代码</summary>

<<< @/utils/validator/isEmptyLine.vue

</details>

#### <divider-param /> {#param-isEmptyLine}

| 参数属性 | 说明       | 类型   | 默认值 |
|----------|------------|--------|--------|
| str      | 待校验字符串 | string | 无     |

| 返回值   | 说明           |
|----------|----------------|
| `boolean`| 是否为空行（仅空白字符） |

#### <divider-desc /> {#desc-isEmptyLine}

- 校验字符串是否为空行（仅空白字符）

</div>

### isIPv4

判断是否为合法IPv4地址

<div class="buzzts-border">

#### <divider-base /> {#base-isIPv4}

<isIPv4 />

<details>
<summary>查看代码</summary>

<<< @/utils/validator/isIPv4.vue

</details>

#### <divider-param /> {#param-isIPv4}

| 参数属性 | 说明           | 类型   | 默认值 |
|----------|----------------|--------|--------|
| str      | 待校验字符串   | string | 无     |

| 返回值   | 说明            |
|----------|-----------------|
| boolean  | 是否为合法IPv4地址 |

#### <divider-desc /> {#desc-isIPv4}

- 校验字符串是否符合IPv4地址格式

</div>

### isIPv6

校验字符串是否为合法IPv6地址（支持完整和压缩格式，排除IPv4）

<div class="buzzts-border">

#### <divider-base /> {#base-isIPv6}

<isIPv6 />

<details>
<summary>查看代码</summary>

<<< @/utils/validator/isIPv6.vue

</details>

#### <divider-param /> {#param-isIPv6}

| 参数属性 | 说明       | 类型   | 默认值 |
|----------|------------|--------|--------|
| str      | 待校验字符串 | string | 无     |

| 返回值   | 说明           |
|----------|----------------|
| `boolean`| 是否为合法IPv6地址 |

#### <divider-desc /> {#desc-isIPv6}

- 校验字符串是否为IPv6地址，支持完整和压缩格式
- 排除IPv4地址格式

</div>

### isEmail

校验字符串是否为合法邮箱格式

<div class="buzzts-border">

#### <divider-base /> {#base-isEmail}

<isEmail />

<details>
<summary>查看代码</summary>

<<< @/utils/validator/isEmail.vue

</details>

#### <divider-param /> {#param-isEmail}

| 参数属性 | 说明       | 类型   | 默认值 |
|----------|------------|--------|--------|
| str      | 待校验邮箱字符串 | string | 无     |

| 返回值   | 说明                   |
|----------|------------------------|
| `boolean`| 是否为合法邮箱格式      |

#### <divider-desc /> {#desc-isEmail}

- 校验字符串是否为合法邮箱格式

</div>

### isFunction

判断是否为函数

<div class="buzzts-border">

#### <divider-base /> {#base-isFunction}

<isFunction />

<details>
<summary>查看代码</summary>

<<< @/utils/validator/isFunction.vue

</details>

#### <divider-param /> {#param-isFunction}

| 参数属性 | 说明     | 类型 | 默认值 |
|----------|----------|------|--------|
| val      | 任意值   | any  | 无     |

| 返回值   | 说明            |
|----------|-----------------|
| boolean  | 是否为函数      |

#### <divider-desc /> {#desc-isFunction}

- 判断传入值类型是否为函数

</div>

### isArray

判断是否为数组

<div class="buzzts-border">

#### <divider-base /> {#base-isArray}

<isArray />

<details>
<summary>查看代码</summary>

<<< @/utils/validator/isArray.vue

</details>

#### <divider-param /> {#param-isArray}

| 参数属性 | 说明   | 类型 | 默认值 |
|----------|--------|------|--------|
| val      | 任意值 | any  | 无     |

| 返回值   | 说明     |
|----------|----------|
| boolean  | 是否数组 |

#### <divider-desc /> {#desc-isArray}

- 判断传入的值是否为数组
</div>

### isObject

判断是否为普通对象（非 null，非数组）

<div class="buzzts-border">

#### <divider-base /> {#base-isObject}

<isObject />

<details>
<summary>查看代码</summary>

<<< @/utils/validator/isObject.vue

</details>

#### <divider-param /> {#param-isObject}

| 参数属性 | 说明   | 类型 | 默认值 |
|----------|--------|------|--------|
| val      | 任意值 | any  | 无     |

| 返回值   | 说明       |
|----------|------------|
| boolean  | 是否普通对象 |

#### <divider-desc /> {#desc-isObject}

- 判断传入的值是否为普通对象（非 null，非数组）
</div>

### isUrl

简单判断是否 URL 格式

<div class="buzzts-border">

#### <divider-base /> {#base-isUrl}

<isUrl />

<details>
<summary>查看代码</summary>

<<< @/utils/validator/isUrl.vue

</details>

#### <divider-param /> {#param-isUrl}

| 参数属性 | 说明           | 类型   | 默认值 |
|----------|----------------|--------|--------|
| url      | 待校验字符串   | string | 无     |

| 返回值   | 说明            |
|----------|-----------------|
| boolean  | 是否为 URL 格式 |

#### <divider-desc /> {#desc-isUrl}

- 利用 try-catch 方式判断字符串是否为合法 URL

</div>

### isSymbol

判断是否为 Symbol 类型

<div class="buzzts-border">

#### <divider-base /> {#base-isSymbol}

<isSymbol />

<details>
<summary>查看代码</summary>

<<< @/utils/validator/isSymbol.vue

</details>

#### <divider-param /> {#param-isSymbol}

| 参数属性 | 说明       | 类型 | 默认值 |
|----------|------------|------|--------|
| val      | 任意值     | any  | 无     |

| 返回值   | 说明           |
|----------|----------------|
| boolean  | 是否 Symbol 类型 |

#### <divider-desc /> {#desc-isSymbol}

- 判断传入值是否为 Symbol 类型
- 示例：
  - `isSymbol(Symbol()) // true`
  - `isSymbol('abc') // false`

</div>

### isBigInt

判断是否为 BigInt 类型

<div class="buzzts-border">

#### <divider-base /> {#base-isBigInt}

<isBigInt />

<details>
<summary>查看代码</summary>

<<< @/utils/validator/isBigInt.vue

</details>

#### <divider-param /> {#param-isBigInt}

| 参数属性 | 说明   | 类型   | 默认值    |
|----------|--------|--------|-----------|
| val      | 任意值 | any    | 无        |

| 返回值   | 说明           |
|----------|----------------|
| `boolean`| 是否 BigInt 类型|

#### <divider-desc /> {#desc-isBigInt}

- 判断输入值是否为 BigInt 类型
- 示例：
  - `isBigInt(BigInt(123)) // true`
  - `isBigInt(123) // false`

</div>

### getTypeOf

获取参数类型，支持基本类型和常见内置对象类型

<div class="buzzts-border">

#### <divider-base /> {#base-getTypeOf}

<getTypeOf />

<details>
<summary>查看代码</summary>

<<< @/utils/validator/getTypeOf.vue

</details>

#### <divider-param /> {#param-getTypeOf}

| 参数属性 | 说明           | 类型    | 默认值 |
|----------|----------------|---------|--------|
| param    | 需要判断类型的参数 | unknown | 无     |

| 返回值   | 说明                   |
|----------|------------------------|
| `string` | 返回参数的具体类型名称（首字母大写）|

#### <divider-desc /> {#desc-getTypeOf}

- 利用 `Object.prototype.toString` 获取类型标签
- 返回首字母大写的类型名称，如 `"String"`, `"Array"`, `"AsyncFunction"` 等
- 示例：
  - `getTypeOf('abc') // "String"`
  - `getTypeOf([]) // "Array"`

</div>

### isDataTime

简单时间格式校验，支持日期和时间部分

<div class="buzzts-border">

#### <divider-base /> {#base-isDataTime}

<isDataTime />

<details>
<summary>查看代码</summary>

<<< @/utils/validator/isDataTime.vue

</details>

#### <divider-param /> {#param-isDataTime}

| 参数属性 | 说明         | 类型   | 默认值 |
|----------|--------------|--------|--------|
| str      | 待校验字符串 | string | 无     |

| 返回值   | 说明           |
|----------|----------------|
| boolean  | 是否为简单时间格式 |

#### <divider-desc /> {#desc-isDataTime}

- 简单时间格式校验，支持日期和时间部分
</div>

### isChineseIDCardNumber

支持第一代15位和第二代18位身份证号校验

<div class="buzzts-border">

#### <divider-base /> {#base-isChineseIDCardNumber}

<isChineseIDCardNumber />

<details>
<summary>查看代码</summary>

<<< @/utils/validator/isChineseIDCardNumber.vue

</details>

#### <divider-param /> {#param-isChineseIDCardNumber}

| 参数属性 | 说明                 | 类型           | 默认值 |
|----------|----------------------|----------------|--------|
| str      | 身份证号             | string         | 无     |

| 返回值   | 说明           |
|----------|----------------|
| boolean  | 是否符合身份证号格式 |

#### <divider-desc /> {#desc-isChineseIDCardNumber}

- 支持第一代15位和第二代18位身份证号校验
</div>

### isPostCode

校验是否是大陆邮政编码

<div class="buzzts-border">

#### <divider-base /> {#base-isPostCode}

<isPostCode />

<details>
<summary>查看代码</summary>

<<< @/utils/validator/isPostCode.vue

</details>

#### <divider-param /> {#param-isPostCode}

| 参数属性 | 说明           | 类型             | 默认值 |
|----------|----------------|------------------|--------|
| value    | 待校验值       | number \| string | 无     |

| 返回值   | 说明           |
|----------|----------------|
| boolean  | 是否为大陆邮政编码 |

#### <divider-desc /> {#desc-isPostCode}

- 校验是否是大陆邮政编码
</div>

### isTelNumber

是否是手机号

<div class="buzzts-border">

#### <divider-base /> {#base-isTelNumber}

<isTelNumber />

<details>
<summary>查看代码</summary>

<<< @/utils/validator/isTelNumber.vue

</details>

#### <divider-param /> {#param-isTelNumber}

| 参数属性 | 说明         | 类型   | 默认值 |
|----------|--------------|--------|--------|
| str      | 待校验字符串 | string | 无     |

| 返回值   | 说明     |
|----------|----------|
| boolean  | 是否是手机号 |

#### <divider-desc /> {#desc-isTelNumber}

- 校验字符串是否为合法手机号
</div>

### isHasEmoji

是否包含emoji表情

<div class="buzzts-border">

#### <divider-base /> {#base-isHasEmoji}

<isHasEmoji />

<details>
<summary>查看代码</summary>

<<< @/utils/validator/isHasEmoji.vue

</details>

#### <divider-param /> {#param-isHasEmoji}

| 参数属性 | 说明         | 类型   | 默认值 |
|----------|--------------|--------|--------|
| value    | 待校验字符串 | string | 无     |

| 返回值   | 说明           |
|----------|----------------|
| boolean  | 是否包含emoji表情 |

#### <divider-desc /> {#desc-isHasEmoji}

- 判断字符串是否包含emoji表情
</div>

### isHexColor

校验是否为十六进制颜色字符串，支持3位和6位，支持大小写，必须以#开头

<div class="buzzts-border">

#### <divider-base /> {#base-isHexColor}

<isHexColor />

<details>
<summary>查看代码</summary>

<<< @/utils/validator/isHexColor.vue

</details>

#### <divider-param /> {#param-isHexColor}

| 参数属性 | 说明         | 类型   | 默认值 |
|----------|--------------|--------|--------|
| str      | 待校验颜色字符串 | string | 无     |

| 返回值   | 说明           |
|----------|----------------|
| boolean  | 是否为合法十六进制颜色字符串 |

#### <divider-desc /> {#desc-isHexColor}

- 支持3位或6位十六进制颜色，必须以#开头，支持大小写字母
</div>

### isNLen

校验字符串是否为指定长度的任意字符字符串

<div class="buzzts-border">

#### <divider-base /> {#base-isNLen}

<isNLen />

<details>
<summary>查看代码</summary>

<<< @/utils/validator/isNLen.vue

</details>

#### <divider-param /> {#param-isNLen}

| 参数属性 | 说明         | 类型   | 默认值 |
|----------|--------------|--------|--------|
| str      | 待校验字符串 | string | 无     |
| n        | 指定长度     | number | 无     |

| 返回值   | 说明                         |
|----------|------------------------------|
| `boolean`| 是否为指定长度的任意字符字符串 |

#### <divider-desc /> {#desc-isNLen}

- 校验字符串是否为长度为n的任意字符字符串

</div>

### isEnCharacter

校验字符串是否全部为英文字符（大小写均可）

<div class="buzzts-border">

#### <divider-base /> {#base-isEnCharacter}

<isEnCharacter />

<details>
<summary>查看代码</summary>

<<< @/utils/validator/isEnCharacter.vue

</details>

#### <divider-param /> {#param-isEnCharacter}

| 参数属性 | 说明       | 类型   | 默认值 |
|----------|------------|--------|--------|
| str      | 待校验字符串 | string | 无     |

| 返回值   | 说明                   |
|----------|------------------------|
| `boolean`| 是否全部为英文字符（大小写均可） |

#### <divider-desc /> {#desc-isEnCharacter}

- 校验字符串是否全部为英文字符（大小写均可）

</div>

### isUpEnCharacter

校验字符串是否全部为大写英文字符

<div class="buzzts-border">

#### <divider-base /> {#base-isUpEnCharacter}

<isUpEnCharacter />

<details>
<summary>查看代码</summary>

<<< @/utils/validator/isUpEnCharacter.vue

</details>

#### <divider-param /> {#param-isUpEnCharacter}

| 参数属性 | 说明       | 类型   | 默认值 |
|----------|------------|--------|--------|
| str      | 待校验字符串 | string | 无     |

| 返回值   | 说明                   |
|----------|------------------------|
| `boolean`| 是否全大写英文字符      |

#### <divider-desc /> {#desc-isUpEnCharacter}

- 校验字符串是否全部为大写英文字符

</div>

### isLowerEnCharacter

校验字符串是否全部为小写英文字符

<div class="buzzts-border">

#### <divider-base /> {#base-isLowerEnCharacter}

<isLowerEnCharacter />

<details>
<summary>查看代码</summary>

<<< @/utils/validator/isLowerEnCharacter.vue

</details>

#### <divider-param /> {#param-isLowerEnCharacter}

| 参数属性 | 说明       | 类型   | 默认值 |
|----------|------------|--------|--------|
| str      | 待校验字符串 | string | 无     |

| 返回值   | 说明                   |
|----------|------------------------|
| `boolean`| 是否全小写英文字符      |

#### <divider-desc /> {#desc-isLowerEnCharacter}

- 校验字符串是否全部为小写英文字符

</div>

### isNumberEnCharacter

校验字符串是否只包含数字和英文字符

<div class="buzzts-border">

#### <divider-base /> {#base-isNumberEnCharacter}

<isNumberEnCharacter />

<details>
<summary>查看代码</summary>

<<< @/utils/validator/isNumberEnCharacter.vue

</details>

#### <divider-param /> {#param-isNumberEnCharacter}

| 参数属性 | 说明       | 类型   | 默认值 |
|----------|------------|--------|--------|
| str      | 待校验字符串 | string | 无     |

| 返回值   | 说明                   |
|----------|------------------------|
| `boolean`| 是否只包含数字和英文字符 |

#### <divider-desc /> {#desc-isNumberEnCharacter}

- 校验字符串是否只包含数字和英文字符

</div>

### isNumberEnUnderscores

校验字符串是否只包含数字、英文和下划线

<div class="buzzts-border">

#### <divider-base /> {#base-isNumberEnUnderscores}

<isNumberEnUnderscores />

<details>
<summary>查看代码</summary>

<<< @/utils/validator/isNumberEnUnderscores.vue

</details>

#### <divider-param /> {#param-isNumberEnUnderscores}

| 参数属性 | 说明       | 类型   | 默认值 |
|----------|------------|--------|--------|
| str      | 待校验字符串 | string | 无     |

| 返回值   | 说明                   |
|----------|------------------------|
| `boolean`| 是否只包含数字、英文和下划线 |

#### <divider-desc /> {#desc-isNumberEnUnderscores}

- 校验字符串是否只包含数字、英文和下划线

</div>

### isIsContainSpecialCharacter

校验字符串是否包含特殊字符

<div class="buzzts-border">

#### <divider-base /> {#base-isIsContainSpecialCharacter}

<isIsContainSpecialCharacter />

<details>
<summary>查看代码</summary>

<<< @/utils/validator/isIsContainSpecialCharacter.vue

</details>

#### <divider-param /> {#param-isIsContainSpecialCharacter}

| 参数属性 | 说明       | 类型   | 默认值 |
|----------|------------|--------|--------|
| str      | 待校验字符串 | string | 无     |

| 返回值   | 说明                   |
|----------|------------------------|
| `boolean`| 是否包含特殊字符        |

#### <divider-desc /> {#desc-isIsContainSpecialCharacter}

- 校验字符串是否包含特殊字符

</div>

### isDoubleByte

校验字符串是否包含双字节字符

<div class="buzzts-border">

#### <divider-base /> {#base-isDoubleByte}

<isDoubleByte />

<details>
<summary>查看代码</summary>

<<< @/utils/validator/isDoubleByte.vue

</details>

#### <divider-param /> {#param-isDoubleByte}

| 参数属性 | 说明       | 类型   | 默认值 |
|----------|------------|--------|--------|
| str      | 待校验字符串 | string | 无     |

| 返回值   | 说明           |
|----------|----------------|
| `boolean`| 是否包含双字节字符 |

#### <divider-desc /> {#desc-isDoubleByte}

- 校验字符串是否包含双字节字符

</div>

### isHex

校验字符串是否为十六进制字符串

<div class="buzzts-border">

#### <divider-base /> {#base-isHex}

<isHex />

<details>
<summary>查看代码</summary>

<<< @/utils/validator/isHex.vue

</details>

#### <divider-param /> {#param-isHex}

| 参数属性 | 说明       | 类型   | 默认值 |
|----------|------------|--------|--------|
| str      | 待校验字符串 | string | 无     |

| 返回值   | 说明                   |
|----------|------------------------|
| `boolean`| 是否为十六进制字符串 |

#### <divider-desc /> {#desc-isHex}

- 校验字符串是否只包含十六进制字符

</div>

### isChines

校验字符串是否是中文

<div class="buzzts-border">

#### <divider-base /> {#base-isChines}

<isChines />

<details>
<summary>查看代码</summary>

<<< @/utils/validator/isChines.vue

</details>

#### <divider-param /> {#param-isChines}

| 参数属性 | 说明       | 类型   | 默认值 |
|----------|------------|--------|--------|
| str      | 待校验字符串 | string | 无     |

| 返回值   | 说明           |
|----------|----------------|
| `boolean`| 是否是中文 |

#### <divider-desc /> {#desc-isChines}

- 校验字符串是否是中文

</div>
