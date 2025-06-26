<script setup>
import { useAddNumInOutlineLabel } from '../../.vitepress/utils/createElement.ts'
useAddNumInOutlineLabel(40)

import randInt from "./randInt.vue"
import randFloat from "./randFloat.vue"
import randPositiveInt from "./randPositiveInt.vue"
import randPositiveFloat from "./randPositiveFloat.vue"
import randBool from "./randBool.vue"  
import randBoolWeighted from "./randBoolWeighted.vue"
import randNumber from "./randNumber.vue"  
import randHex from "./randHex.vue"  
import nanoidGenerator from "./nanoidGenerator.vue"  
import randString from "./randString.vue"  
import randTime from "./randTime.vue"  
import randPastTime from "./randPastTime.vue"  
import randTimeBetween from "./randTimeBetween.vue"
import randTimestamp from "./randTimestamp.vue"  
import randISOTime from "./randISOTime.vue"  
import randDate from "./randDate.vue"  
import rangeWithStep from "./rangeWithStep.vue"  
import randColorCMYK from "./randColorCMYK.vue"  
import randColorHEX from "./randColorHEX.vue"  
import randColorHSL from "./randColorHSL.vue"  
import randColorRGB from "./randColorRGB.vue"
import randColorHexShort from "./randColorHexShort.vue"
import randUniformArray from "./randUniformArray.vue"
import randSelectWeighted from "./randSelectWeighted.vue"
import randSample from "./randSample.vue"
import randUniqueSample from "./randUniqueSample.vue"
import randShuffle from "./randShuffle.vue"
import randBernoulli from "./randBernoulli.vue"
import randBinomial from "./randBinomial.vue"
import randPoisson from "./randPoisson.vue"
import randExponential from "./randExponential.vue"
import randIPv4 from "./randIPv4.vue"
import randIPv6 from "./randIPv6.vue"
import randMAC from "./randMAC.vue"
import randAngle from "./randAngle.vue"
import randCirclePointInside from "./randCirclePointInside.vue"
import randEmail from "./randEmail.vue"
import randUUIDv1 from "./randUUIDv1.vue"
import randUUIDv4 from "./randUUIDv4.vue"

</script>

::: tip 支持任意 `JavaScript` 环境或框架
随机数生成工具集（全面支持正负数范围）
:::

## 基础随机函数

### randInt

生成指定范围内的随机整数（包含最小值，不包含最大值）

<div class="buzzts-border">

#### <divider-base /> {#base1}

<randInt />

<details>
<summary>查看代码</summary>

<<< @/utils/random/randInt.vue

</details>

#### <divider-param /> {#param1}

| 参数属性 | 说明               | 类型     | 默认值 |
|----------|--------------------|----------|--------|
| `min`    | 最小值（包含）     | `number` | -      |
| `max`    | 最大值（不包含）   | `number` | -      |

| 返回值   | 说明               |
|----------|--------------------|
| `number` | 范围内的随机整数   |

#### <divider-desc /> {#desc1}

- 自动处理 `min > max` 的情况
- 边界值安全：`randInt(5,5)` 返回 5
- 支持正数、负数及跨零范围
- 可通过开关限制仅生成正数
</div>

### randFloat

生成指定范围内的随机浮点数（高精度）

<div class="buzzts-border">

#### <divider-base /> {#base2}

<randFloat />

<details>
<summary>查看代码</summary>

<<< @/utils/random/randFloat.vue

</details>

#### <divider-param /> {#param2}

| 参数属性    | 说明               | 类型     | 默认值 |
|-------------|--------------------|----------|--------|
| `min`       | 最小值（包含）     | `number` | -      |
| `max`       | 最大值（不包含）   | `number` | -      |
| `precision` | 小数位数           | `number` | 16     |

| 返回值   | 说明               |
|----------|--------------------|
| `number` | 范围内的随机浮点数 |

#### <divider-desc /> {#desc2}

- 精度可达 16 位小数
- 支持正数、负数及跨零范围
- 可通过开关限制仅生成正数
- 自动处理边界条件和参数顺序
</div>

### randNumber

生成指定长度的随机数字字符串

<div class="buzzts-border">

<randNumber />

<details>
<summary>查看代码</summary>

<<< @/utils/random/randNumber.vue

</details>

#### 参数说明

| 参数属性 | 说明               | 类型     | 默认值            |
|----------|--------------------|----------|-------------------|
| `length` | 生成字符串长度     | `number` | -                 |
| `customBytes` | 自定义数字字符集 | `string` | `"0123456789"` |

| 返回值 | 说明               |
|--------|--------------------|
| `string` | 随机数字字符串    |

#### 说明

- 默认字符集为 `"0123456789"`  
- 支持自定义字符集  
- 适合生成验证码、随机ID等数字字符串场景

</div>

---

### randHex

生成指定字节长度的随机十六进制字符串

<div class="buzzts-border">

<randHex />

<details>
<summary>查看代码</summary>

<<< @/utils/random/randHex.vue

</details>

#### 参数说明

| 参数属性 | 说明               | 类型     | 默认值                       |
|----------|--------------------|----------|------------------------------|
| `bytesLen` | 生成字节长度      | `number` | -                            |
| `customBytes` | 自定义16进制字符集 | `string` | `"ABCDEF0123456789"`          |

| 返回值 | 说明               |
|--------|--------------------|
| `string` | 随机十六进制字符串 |

#### 说明

- 生成的字符串长度是 `bytesLen * 2`  
- 默认字符集为 `"ABCDEF0123456789"`  
- 支持自定义字符集  
- 适合生成随机颜色值、散列前缀等场景

</div>

### randBool

生成随机布尔值，概率均等

<div class="buzzts-border">

#### <divider-base /> {#base5}

<randBool />

<details>
<summary>查看代码</summary>

<<< @/utils/random/randBool.vue

</details>

#### <divider-param /> {#param5}

| 参数属性 | 说明 | 类型 | 默认值 |
|----------|------|------|--------|
| 无       | 无   | 无   | 无     |

| 返回值   | 说明             |
|----------|------------------|
| `boolean`| 随机的布尔值true或false |

#### <divider-desc /> {#desc5}

- 生成概率均等的随机布尔值
- 无需任何参数
- 适合需要随机开关、随机判断等场景
</div>

### randString

基于自定义字符类型掩码和 ASCII 码表的随机字符串生成函数，实现短且唯一的随机 ID。

<div class="buzzts-border">

#### <divider-base /> {#base-randstring}

<randString />

<details>
<summary>查看代码</summary>

<<< @/utils/random/randString.vue

</details>

#### <divider-param /> {#param-randstring}

| 参数属性     | 说明                           | 类型           | 默认值                                   |
|--------------|--------------------------------|----------------|------------------------------------------|
| `length`     | 生成 ID 的长度                 | `number`       | `21`                                     |
| `mode`   | 字符类型掩码，支持多选：<br>`RandType.LOWERCASE\|RandType.SPECIAL`<br>（小写字母和特殊字符） | `RandType` |`RandType.CAPITAL \| RandType.NUMBER`（大写字母和数字） |

| 返回值       | 说明                           |
|--------------|--------------------------------|
| `string`     | 生成的随机 ID 字符串           |

#### <divider-desc /> {#desc-randstring}

- 默认支持大写字母、小写字母、数字和特殊字符四种类型的字符组合
- 通过掩码 `mode` 灵活控制字符类型组合，满足不同业务需求
- 纯前端实现，无需依赖浏览器 Crypto API，兼容性强
- 适合生成短小且唯一的随机 ID，用于验证码、短链接、唯一标识等场景
- 生成速度快，代码简洁易维护

</div>

### rangeWithStep

接收两个数字作为区间边界，自动规范顺序，支持 `min` 大于 `max` 的情况，返回该区间内所有整数的数组，保证从小到大排列。

<div class="buzzts-border">

#### <divider-base /> {#base-rangeWithStep}

<rangeWithStep />

<details>
<summary>查看代码</summary>

<<< @/utils/random/rangeWithStep.vue

</details>

#### <divider-param /> {#param-rangeWithStep}

| 参数属性 | 说明               | 类型     | 默认值 |
|----------|--------------------|----------|--------|
| `min`   | 区间的起始值       | `number` | —      |
| `max`   | 区间的结束值       | `number` | —      |

| 返回值   | 说明                     |
|----------|--------------------------|
| `number[]` | 包含区间内所有整数的数组，保证从小到大排列 |

#### <divider-desc /> {#desc-rangeWithStep}

- 返回包含区间内所有**整数**的数组，顺序从小到大
- 适用于需要整数区间列表的场景，如分页页码、区间遍历等
- 代码简洁，性能高效，易于维护和复用

</div>

### randColorRGB

生成随机 RGB 颜色字符串，格式为 "rgb(r, g, b)"

<div class="buzzts-border">

#### <divider-base /> {#base-rgb}

<randColorRGB />

<details>
<summary>查看代码</summary>

<<< @/utils/random/randColorRGB.vue

</details>

#### <divider-param /> {#param-rgb}

| 参数属性 | 说明                   | 类型           | 默认值     |
|----------|------------------------|----------------|------------|
| `rRange` | 红色通道范围           | [number, number] | [0, 255]   |
| `gRange` | 绿色通道范围           | [number, number] | [0, 255]   |
| `bRange` | 蓝色通道范围           | [number, number] | [0, 255]   |

| 返回值   | 说明                       |
|----------|----------------------------|
| `string` | 格式为 "rgb(r, g, b)"，r/g/b取值区间由参数决定，默认0~255 |

#### <divider-desc /> {#desc-rgb}

- 生成随机的 RGB 颜色字符串
- 支持指定每个颜色通道的取值范围，默认0~255
- 适合需要随机颜色显示、测试等场景

</div>

---

### randColorCMYK

生成随机 CMYK 颜色字符串，格式为 "cmyk(c%, m%, y%, k%)"

<div class="buzzts-border">

#### <divider-base /> {#base-cmyk}

<randColorCMYK />

<details>
<summary>查看代码</summary>

<<< @/utils/random/randColorCMYK.vue

</details>

#### <divider-param /> {#param-cmyk}

| 参数属性 | 说明                   | 类型           | 默认值     |
|----------|------------------------|----------------|------------|
| `cRange` | 青色通道范围           | [number, number] | [0, 100]   |
| `mRange` | 品红通道范围           | [number, number] | [0, 100]   |
| `yRange` | 黄色通道范围           | [number, number] | [0, 100]   |
| `kRange` | 黑色通道范围           | [number, number] | [0, 100]   |

| 返回值   | 说明                          |
|----------|-------------------------------|
| `string` | 格式为 "cmyk(c%, m%, y%, k%)"，四个通道取值区间由参数决定，默认0~100% |

#### <divider-desc /> {#desc-cmyk}

- 生成随机的 CMYK 颜色字符串
- 支持指定每个通道的取值范围，默认0~100%
- 适合打印颜色模拟、设计测试等场景

</div>

---

### randColorHSL

生成随机 HSL 颜色字符串，格式为 "hsl(h, s%, l%)"

<div class="buzzts-border">

#### <divider-base /> {#base-hsl}

<randColorHSL />

<details>
<summary>查看代码</summary>

<<< @/utils/random/randColorHSL.vue

</details>

#### <divider-param /> {#param-hsl}

| 参数属性 | 说明                   | 类型           | 默认值     |
|----------|------------------------|----------------|------------|
| `hRange` | 色调范围               | [number, number] | [0, 360]   |
| `sRange` | 饱和度范围             | [number, number] | [0, 100]   |
| `lRange` | 亮度范围               | [number, number] | [0, 100]   |

| 返回值   | 说明                       |
|----------|----------------------------|
| `string` | 格式为 "hsl(h, s%, l%)"，h/s/l取值区间由参数决定，默认h:0~360，s/l:0~100% |

#### <divider-desc /> {#desc-hsl}

- 生成随机的 HSL 颜色字符串
- 支持指定色调、饱和度、亮度的取值范围，默认分别为0~360，0~100%，0~100%
- 适合色彩调整、动画渐变等场景

</div>

### randColorHEX

生成随机 HEX 颜色字符串，带 "#" 前缀

<div class="buzzts-border">

#### <divider-base /> {#base-hex}

<randColorHEX />

<details>
<summary>查看代码</summary>

<<< @/utils/random/randColorHEX.vue

</details>

#### <divider-param /> {#param-hex}

| 参数属性       | 说明                             | 类型   | 默认值            |
|----------------|---------------------------------|--------|-------------------|
| `length`       | 生成的 HEX 字符串长度           | number | 6                 |
| `customHexChars`| 自定义16进制字符集（可选）      | string | "0123456789ABCDEF" |

| 返回值   | 说明                              |
|----------|-----------------------------------|
| `string` | 带 "#" 前缀的随机 HEX 颜色字符串  |

#### <divider-desc /> {#desc-hex}

- 生成指定长度的随机 HEX 颜色字符串
- 默认长度6，表示标准的 #RRGGBB 格式
- 支持自定义16进制字符集
- 适合网页颜色随机、主题色生成等场景

</div>


### randColorHexShort

生成短格式HEX颜色字符串

<div class="buzzts-border">

#### <divider-base /> {#base-randColorHexShort}

<randColorHexShort />

<details>
<summary>查看代码</summary>

<<< @/utils/random/randColorHexShort.vue

</details>

#### <divider-param /> {#param-randColorHexShort}

| 参数属性 | 说明               | 类型   | 默认值             |
|----------|--------------------|--------|--------------------|
| hex      | HEX字符串长度，默认0123456789abcdef | string | "0123456789abcdef" |

| 返回值   | 说明           |
|----------|----------------|
| `string` | 三位短HEX颜色字符串，如"#abc" |

#### <divider-desc /> {#desc-randColorHexShort}

- 生成三位短格式HEX颜色字符串
- 默认使用16进制数字和字母a-f

</div>

### randUniformArray

生成指定长度，元素在[min,max]均匀分布的随机浮点数组

<div class="buzzts-border">

#### <divider-base /> {#base-randUniformArray}

<randUniformArray />

<details>
<summary>查看代码</summary>

<<< @/utils/random/randUniformArray.vue

</details>

#### <divider-param /> {#param-randUniformArray}

| 参数属性 | 说明   | 类型   | 默认值 |
|----------|--------|--------|--------|
| length   | 数组长度 | number | 无     |
| min      | 最小值 | number | 0      |
| max      | 最大值 | number | 1      |

| 返回值   | 说明           |
|----------|----------------|
| `number[]` | 均匀分布随机数组 |

#### <divider-desc /> {#desc-randUniformArray}

- 生成指定长度的随机浮点数组
- 数组元素在[min,max]区间均匀分布

</div>

### randSelectWeighted

根据权重数组随机选取一个元素

<div class="buzzts-border">

#### <divider-base /> {#base-randSelectWeighted}

<randSelectWeighted />

<details>
<summary>查看代码</summary>

<<< @/utils/random/randSelectWeighted.vue

</details>

#### <divider-param /> {#param-randSelectWeighted}

| 参数属性 | 说明         | 类型     | 默认值 |
|----------|--------------|----------|--------|
| items    | 选项数组     | any[]    | 无     |
| weights  | 权重数组，长度与items相同 | number[] | 无     |

| 返回值   | 说明           |
|----------|----------------|
| `any`    | 根据权重随机选中的元素 |

#### <divider-desc /> {#desc-randSelectWeighted}

- 根据权重数组随机选取一个元素
- 权重越大，选中概率越高

</div>

### randSample

从数组中随机抽取n个元素，可能重复

<div class="buzzts-border">

#### <divider-base /> {#base-randSample}

<randSample />

<details>
<summary>查看代码</summary>

<<< @/utils/random/randSample.vue

</details>

#### <divider-param /> {#param-randSample}

| 参数属性 | 说明     | 类型   | 默认值 |
|----------|----------|--------|--------|
| array    | 源数组   | any[]  | 无     |
| n        | 抽样数量 | number | 无     |

| 返回值   | 说明           |
|----------|----------------|
| `any[]`  | 随机抽样结果，允许重复 |

#### <divider-desc /> {#desc-randSample}

- 从数组中随机抽取n个元素
- 抽样允许重复

</div>

### randUniqueSample

从数组中随机抽取n个不重复元素，n不得大于数组长度

<div class="buzzts-border">

#### <divider-base /> {#base-randUniqueSample}

<randUniqueSample />

<details>
<summary>查看代码</summary>

<<< @/utils/random/randUniqueSample.vue

</details>

#### <divider-param /> {#param-randUniqueSample}

| 参数属性 | 说明     | 类型   | 默认值 |
|----------|----------|--------|--------|
| array    | 源数组   | any[]  | 无     |
| n        | 抽样数量 | number | 无     |

| 返回值   | 说明           |
|----------|----------------|
| `any[]`  | 不重复随机抽样结果 |

#### <divider-desc /> {#desc-randUniqueSample}

- 从数组中随机抽取n个不重复元素
- 抽样数量n不得大于数组长度

</div>

### randShuffle

对数组进行随机洗牌，返回新数组

<div class="buzzts-border">

#### <divider-base /> {#base-randShuffle}

<randShuffle />

<details>
<summary>查看代码</summary>

<<< @/utils/random/randShuffle.vue

</details>

#### <divider-param /> {#param-randShuffle}

| 参数属性 | 说明     | 类型   | 默认值 |
|----------|----------|--------|--------|
| array    | 待打乱数组 | any[]  | 无     |

| 返回值   | 说明           |
|----------|----------------|
| `any[]`  | 打乱后的新数组 |

#### <divider-desc /> {#desc-randShuffle}

- 对数组进行随机洗牌
- 返回打乱顺序的新数组，不修改原数组

</div>

### randBoolWeighted

根据概率p生成随机布尔值，默认均等概率

<div class="buzzts-border">

#### <divider-base /> {#base-randBoolWeighted}

<randBoolWeighted />

<details>
<summary>查看代码</summary>

<<< @/utils/random/randBoolWeighted.vue

</details>

#### <divider-param /> {#param-randBoolWeighted}

| 参数属性 | 说明               | 类型   | 默认值 |
|----------|--------------------|--------|--------|
| p        | 返回true的概率，范围0~1 | number | 0.5    |

| 返回值   | 说明           |
|----------|----------------|
| `boolean`| 随机布尔值     |

#### <divider-desc /> {#desc-randBoolWeighted}

- 根据概率p生成随机布尔值
- p越大，返回true的概率越高

</div>

### randBernoulli

根据伯努利分布生成布尔值，true概率为p

<div class="buzzts-border">

#### <divider-base /> {#base-randBernoulli}

<randBernoulli />

<details>
<summary>查看代码</summary>

<<< @/utils/random/randBernoulli.vue

</details>

#### <divider-param /> {#param-randBernoulli}

| 参数属性 | 说明           | 类型   | 默认值 |
|----------|----------------|--------|--------|
| p        | 事件发生概率，0~1之间 | number | 无     |

| 返回值   | 说明           |
|----------|----------------|
| `boolean`| 随机布尔值，true概率为p |

#### <divider-desc /> {#desc-randBernoulli}

- 按照伯努利分布生成布尔值
- true的概率为参数p

</div>

### randBinomial

生成符合二项分布的随机数

<div class="buzzts-border">

#### <divider-base /> {#base-randBinomial}

<randBinomial />

<details>
<summary>查看代码</summary>

<<< @/utils/random/randBinomial.vue

</details>

#### <divider-param /> {#param-randBinomial}

| 参数属性 | 说明           | 类型   | 默认值 |
|----------|----------------|--------|--------|
| n        | 试验次数       | number | 无     |
| p        | 单次成功概率   | number | 无     |

| 返回值   | 说明           |
|----------|----------------|
| `number` | 二项分布随机数 |

#### <divider-desc /> {#desc-randBinomial}

- 生成符合二项分布的随机数
- 参数n为试验次数，p为单次成功概率

</div>

### randPoisson

生成符合泊松分布的随机整数

<div class="buzzts-border">

#### <divider-base /> {#base-randPoisson}

<randPoisson />

<details>
<summary>查看代码</summary>

<<< @/utils/random/randPoisson.vue

</details>

#### <divider-param /> {#param-randPoisson}

| 参数属性 | 说明           | 类型   | 默认值 |
|----------|----------------|--------|--------|
| lambda   | 泊松分布参数，平均事件数 | number | 无     |

| 返回值   | 说明           |
|----------|----------------|
| `number` | 泊松分布随机数 |

#### <divider-desc /> {#desc-randPoisson}

- 生成符合泊松分布的随机整数
- 参数lambda为平均事件数

</div>

### randExponential

生成符合指数分布的随机数

<div class="buzzts-border">

#### <divider-base /> {#base-randExponential}

<randExponential />

<details>
<summary>查看代码</summary>

<<< @/utils/random/randExponential.vue

</details>

#### <divider-param /> {#param-randExponential}

| 参数属性 | 说明           | 类型   | 默认值 |
|----------|----------------|--------|--------|
| lambda   | 指数分布参数，正数 | number | 无     |

| 返回值   | 说明           |
|----------|----------------|
| `number` | 指数分布随机数 |

#### <divider-desc /> {#desc-randExponential}

- 生成符合指数分布的随机数
- 参数lambda为分布参数

</div>

### randIPv4

生成合法的随机IPv4地址

<div class="buzzts-border">

#### <divider-base /> {#base-randIPv4}

<randIPv4 />

<details>
<summary>查看代码</summary>

<<< @/utils/random/randIPv4.vue

</details>

#### <divider-param /> {#param-randIPv4}

| 参数属性 | 说明 | 类型 | 默认值 |
|----------|------|------|--------|
| 无       | 无   | 无   | 无     |

| 返回值   | 说明           |
|----------|----------------|
| `string` | 随机IPv4地址字符串 |

#### <divider-desc /> {#desc-randIPv4}

- 生成合法的随机IPv4地址字符串
- 由4个0~255的数字组成

</div>

### randIPv6

生成合法的随机IPv6地址（简化版）

<div class="buzzts-border">

#### <divider-base /> {#base-randIPv6}

<randIPv6 />

<details>
<summary>查看代码</summary>

<<< @/utils/random/randIPv6.vue

</details>

#### <divider-param /> {#param-randIPv6}

| 参数属性 | 说明 | 类型 | 默认值 |
|----------|------|------|--------|
| 无       | 无   | 无   | 无     |

| 返回值   | 说明           |
|----------|----------------|
| `string` | 随机IPv6地址字符串 |

#### <divider-desc /> {#desc-randIPv6}

- 生成合法的随机IPv6地址字符串
- 简化实现，8组16位16进制数

</div>

### randMAC

生成随机MAC地址，首字节最低位为0（非多播）

<div class="buzzts-border">

#### <divider-base /> {#base-randMAC}

<randMAC />

<details>
<summary>查看代码</summary>

<<< @/utils/random/randMAC.vue

</details>

#### <divider-param /> {#param-randMAC}

| 参数属性 | 说明 | 类型 | 默认值 |
|----------|------|------|--------|
| 无       | 无   | 无   | 无     |

| 返回值   | 说明           |
|----------|----------------|
| `string` | 随机MAC地址字符串 |

#### <divider-desc /> {#desc-randMAC}

- 生成随机MAC地址
- 首字节最低位固定为0，表示单播地址

</div>

### randAngle

生成0~360度的随机角度

<div class="buzzts-border">

#### <divider-base /> {#base-randAngle}

<randAngle />

<details>
<summary>查看代码</summary>

<<< @/utils/random/randAngle.vue

</details>

#### <divider-param /> {#param-randAngle}

| 参数属性 | 说明 | 类型 | 默认值 |
|----------|------|------|--------|
| 无       | 无   | 无   | 无     |

| 返回值   | 说明           |
|----------|----------------|
| `number` | 0~360度随机角度 |

#### <divider-desc /> {#desc-randAngle}

- 生成范围在0到360度之间的随机角度

</div>

### randCirclePointInside

生成圆内均匀分布的随机点坐标

<div class="buzzts-border">

#### <divider-base /> {#base-randCirclePointInside}

<randCirclePointInside />

<details>
<summary>查看代码</summary>

<<< @/utils/random/randCirclePointInside.vue

</details>

#### <divider-param /> {#param-randCirclePointInside}

| 参数属性 | 说明     | 类型   | 默认值 |
|----------|----------|--------|--------|
| radius   | 圆半径   | number | 无     |

| 返回值   | 说明           |
|----------|----------------|
| `{x:number,y:number}` | 圆内随机点坐标 |

#### <divider-desc /> {#desc-randCirclePointInside}

- 生成圆内均匀分布的随机点
- 返回点的x,y坐标

</div>

### randEmail

生成随机邮箱地址，用户名部分为随机字符串

<div class="buzzts-border">

#### <divider-base /> {#base-randEmail}

<randEmail />

<details>
<summary>查看代码</summary>

<<< @/utils/random/randEmail.vue

</details>

#### <divider-param /> {#param-randEmail}

| 参数属性 | 说明     | 类型   | 默认值       |
|----------|----------|--------|--------------|
| domain   | 邮箱域名 | string | "example.com" |

| 返回值   | 说明           |
|----------|----------------|
| `string` | 随机邮箱地址字符串 |

#### <divider-desc /> {#desc-randEmail}

- 生成随机邮箱地址
- 用户名为随机字符串，域名可指定

</div>

### randUUIDv1

生成基于时间的UUID v1，非严格实现，仅模拟效果

<div class="buzzts-border">

#### <divider-base /> {#base-randUUIDv1}

<randUUIDv1 />

<details>
<summary>查看代码</summary>

<<< @/utils/random/randUUIDv1.vue

</details>

#### <divider-param /> {#param-randUUIDv1}

| 参数属性 | 说明 | 类型 | 默认值 |
|----------|------|------|--------|
| 无       | 无   | 无   | 无     |

| 返回值   | 说明           |
|----------|----------------|
| `string` | UUID v1格式字符串 |

#### <divider-desc /> {#desc-randUUIDv1}

- 生成基于时间和随机数的UUID v1格式字符串
- 非严格标准实现，仅模拟效果

</div>

### randUUIDv4

生成符合UUID v4标准的随机字符串

<div class="buzzts-border">

#### <divider-base /> {#base-randUUIDv4}

<randUUIDv4 />

<details>
<summary>查看代码</summary>

<<< @/utils/random/randUUIDv4.vue

</details>

#### <divider-param /> {#param-randUUIDv4}

| 参数属性 | 说明 | 类型 | 默认值 |
|----------|------|------|--------|
| 无       | 无   | 无   | 无     |

| 返回值   | 说明           |
|----------|----------------|
| `string` | UUID v4格式字符串 |

#### <divider-desc /> {#desc-randUUIDv4}

- 生成符合UUID v4标准的随机字符串
- 纯随机生成

</div>

### randTime

随机生成未来时间，当前时间加1~1000小时

<div class="buzzts-border">

#### <divider-base /> {#base-randTime}

<randTime />

<details>
<summary>查看代码</summary>

<<< @/utils/random/randTime.vue

</details>

#### <divider-param /> {#param-randTime}

| 参数属性 | 说明       | 类型 | 默认值 |
|----------|------------|------|--------|
| 无       | 无         | 无   | 无     |

| 返回值   | 说明                        |
|----------|-----------------------------|
| `Date`   | 当前时间向后随机若干小时的时间 |

#### <divider-desc /> {#desc-randTime}

- 生成当前时间向后随机1~1000小时的时间
- 无需参数，直接调用生成结果
- 适合需要随机未来时间的场景

</div>


### randPastTime

随机生成过去时间，当前时间减1~1000小时

<div class="buzzts-border">

#### <divider-base /> {#base-randPastTime}

<randPastTime />

<details>
<summary>查看代码</summary>

<<< @/utils/random/randPastTime.vue

</details>

#### <divider-param /> {#param-randPastTime}

| 参数属性 | 说明       | 类型 | 默认值 |
|----------|------------|------|--------|
| 无       | 无         | 无   | 无     |

| 返回值   | 说明                        |
|----------|-----------------------------|
| `Date`   | 当前时间向前随机若干小时的时间 |

#### <divider-desc /> {#desc-randPastTime}

- 生成当前时间向前随机1~1000小时的时间
- 无需参数，直接调用生成结果
- 适合需要随机过去时间的场景

</div>

### randTimeBetween

在指定时间区间内生成随机时间

<div class="buzzts-border">

#### <divider-base /> {#base-randTimeBetween}

<randTimeBetween />

<details>
<summary>查看代码</summary>

<<< @/utils/random/randTimeBetween.vue

</details>

#### <divider-param /> {#param-randTimeBetween}

| 参数属性 | 说明           | 类型   | 默认值 |
|----------|----------------|--------|--------|
| start    | 起始时间       | `Date` | 无     |
| end      | 结束时间       | `Date` | 无     |

| 返回值   | 说明                          |
|----------|-------------------------------|
| `Date`   | 在起始和结束时间之间的随机时间 |

#### <divider-desc /> {#desc-randTimeBetween}

- 生成指定时间区间内的随机时间
- 如果起始时间晚于结束时间会抛出错误
- 适合需要限定时间范围的随机时间生成

</div>

### randISOTime

生成随机 ISO 格式时间字符串

<div class="buzzts-border">

#### <divider-base /> {#base-randISOTime}

<randISOTime />

<details>
<summary>查看代码</summary>

<<< @/utils/random/randISOTime.vue

</details>

#### <divider-param /> {#param-randISOTime}

| 参数属性 | 说明 | 类型 | 默认值 |
|----------|------|------|--------|
| 无       | 无   | 无   | 无     |

| 返回值   | 说明                     |
|----------|--------------------------|
| `string` | 随机生成的 ISO 格式时间字符串 |

#### <divider-desc /> {#desc-randISOTime}

- 生成符合 ISO 8601 标准的随机时间字符串
- 无需任何参数，直接调用生成结果
- 适合需要标准时间格式字符串的场景

</div>

### randTimestamp

生成随机时间戳（单位：毫秒）

<div class="buzzts-border">

#### <divider-base /> {#base-randTimestamp}

<randTimestamp />

<details>
<summary>查看代码</summary>

<<< @/utils/random/randTimestamp.vue

</details>

#### <divider-param /> {#param-randTimestamp}

| 参数属性 | 说明 | 类型 | 默认值 |
|----------|------|------|--------|
| 无       | 无   | 无   | 无     |

| 返回值   | 说明             |
|----------|------------------|
| `number` | 随机生成的时间戳，单位为毫秒 |

#### <divider-desc /> {#desc-randTimestamp}

- 生成一个随机的时间戳（毫秒数）
- 无需参数，直接调用生成结果
- 适合需要时间戳格式的随机时间场景

</div>

### randDate

生成随机日期对象（Date 类型）

<div class="buzzts-border">

#### <divider-base /> {#base-randDate}

<randDate />

<details>
<summary>查看代码</summary>

<<< @/utils/random/randDate.vue

</details>

#### <divider-param /> {#param-randDate}

| 参数属性 | 说明 | 类型 | 默认值 |
|----------|------|------|--------|
| 无       | 无   | 无   | 无     |

| 返回值   | 说明           |
|----------|----------------|
| `Date`   | 随机生成的日期对象 |

#### <divider-desc /> {#desc-randDate}

- 生成一个随机的 `Date` 对象
- 无需参数，直接调用生成结果
- 适合需要随机日期的场景

</div>


## 高阶随机函数

### Nanoid 生成器

基于高效的随机池和自定义字母表实现，生成短且唯一的随机字符串。

<div class="buzzts-border">

#### <divider-base /> {#base-nanoid}

<nanoidGenerator />

<details>
<summary>查看代码</summary>

<<< @/utils/random/nanoidGenerator.vue

</details>

#### <divider-param /> {#param-nanoid}

| 参数属性      | 说明                     | 类型     | 默认值                                   |
|---------------|--------------------------|----------|------------------------------------------|
| `size`        | 生成 ID 的长度           | `number` | `21`                                     |
| `customAlpha` | 自定义字母表字符串       | `string` | 空字符串（使用默认字母表 `ALPHA_BYTES`） |

| 返回值 | 说明                         |
|--------|------------------------------|
| `string` | 生成的随机 ID 字符串         |

#### <divider-desc /> {#desc-nanoid}

- 默认字母表为：`ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789`（大小写字母和数字混合）
- 支持自定义任意字符集生成随机 ID，灵活适配不同场景需求
- 基于浏览器原生 `crypto.getRandomValues` 提供高质量、高性能的随机数生成
- 结合纳秒时间戳（兼容 Node.js 和浏览器环境），保证生成 ID 的单调递增，防止时间回拨导致重复
- 生成的 ID 短小且分布均匀，适用于唯一标识、短链接、验证码等场景
- 相较于 UUID，生成速度更快，且 ID 更短

</div>

### randPositiveInt

生成指定范围内的随机正整数（严格正数范围）

<div class="buzzts-border">

#### <divider-base /> {#base3}

<randPositiveInt />

<details>
<summary>查看代码</summary>

<<< @/utils/random/randPositiveInt.vue

</details>

#### <divider-param /> {#param3}

| 参数属性 | 说明               | 类型     | 默认值 | 限制条件       |
|----------|--------------------|----------|--------|----------------|
| `min`    | 最小正整数（包含） | `number` | 1      | 必须 ≥1        |
| `max`    | 最大正整数（不包含）| `number` | 10     | 必须 > min 且 ≥1 |

| 返回值   | 说明               |
|----------|--------------------|
| `number` | 范围内的随机正整数 |

#### <divider-desc /> {#desc3}

- 专为需要严格正整数的场景设计
- 参数自动验证为有效正整数
- 边界值安全：`randPositiveInt(5,5)` 返回 5
- 比通用 `randInt` 更严格的参数校验
</div>

### randPositiveFloat

生成指定范围内的随机正浮点数（严格正数范围）

<div class="buzzts-border">

#### <divider-base /> {#base4}

<randPositiveFloat />

<details>
<summary>查看代码</summary>

<<< @/utils/random/randPositiveFloat.vue

</details>

#### <divider-param /> {#param4}

| 参数属性    | 说明               | 类型     | 默认值 | 限制条件          |
|-------------|--------------------|----------|--------|-------------------|
| `min`       | 最小正数（包含）   | `number` | 0.1    | 必须 > 0          |
| `max`       | 最大正数（不包含） | `number` | 1.0    | 必须 > min 且 > 0 |
| `precision` | 小数位数           | `number` | 4      | 1-16              |

| 返回值   | 说明               |
|----------|--------------------|
| `number` | 范围内的随机正浮点数 |

#### <divider-desc /> {#desc4}

- 专为需要严格正浮点数的场景设计
- 参数自动验证为有效正数
- 精度可达 16 位小数
- 比通用 `randFloat` 更严格的参数校验
- 自动处理边界条件和参数顺序
</div>

## 专用布尔随机函数

### randBoolWeighted

根据概率生成随机布尔值，支持自定义返回 `true` 的概率。

<div class="buzzts-border">

#### <divider-base /> {#base-weighted}

<randBoolWeighted />

<details>
<summary>查看代码</summary>

<<< @/utils/random/randBoolWeighted.vue

</details>

#### <divider-param /> {#param-weighted}

| 参数属性 | 说明                   | 类型     | 默认值 |
|----------|------------------------|----------|--------|
| `p`      | 返回 `true` 的概率，范围0~1 | `number` | 0.5    |

| 返回值   | 说明               |
|----------|--------------------|
| `boolean`| 根据概率生成的随机布尔值 |

#### <divider-desc /> {#desc-weighted}

- 支持任意概率控制 `true` 的频率  
- `p=0` 总是返回 `false`，`p=1` 总是返回 `true`  
- 适合需要非均等概率随机布尔的场景  
- 简单易用，基于 `Math.random()` 实现

</div>