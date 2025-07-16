<script setup>
import { useAddNumInOutlineLabel } from '../../.vitepress/utils/createElement.ts'
useAddNumInOutlineLabel(7)

import base64ToImageBlob from "./base64ToImageBlob.vue";
import base64ToImageFile from "./base64ToImageFile.vue";
import blobToImageFile from "./blobToImageFile.vue";
import fileToBase64 from "./fileToBase64.vue";
import fileUploader from "./fileUploader.vue";
import getImageFileName from "./getImageFileName.vue";
import urlToImageBlob from "./urlToImageBlob.vue";
import urlToImageFile from "./urlToImageFile.vue";

</script>

::: tip 支持任意 `JavaScript` 环境或框架
处理imagex工具集
:::

### getImageFileName

生成图像文件名

<div class="buzzts-border">

#### <divider-base /> {#base-getImageFileName}

<getImageFileName />

<details>
<summary>查看代码</summary>

<<< @/utils/imagex/getImageFileName.vue

</details>

#### <divider-param /> {#param-getImageFileName}

| 参数属性 | 说明                          | 类型     | 默认值 |
|----------|-------------------------------|----------|--------|
| extension| 文件扩展名（可选）            | `string` | 'png'  |

| 返回值   | 说明                                   |
|----------|----------------------------------------|
| `string` | 返回生成的图像文件名                  |

#### <divider-desc /> {#desc-getImageFileName}

- 生成一个包含当前日期和时间的图像文件名，格式为 `YYYYMMDD_HHMMSS.extension`

</div>

### urlToImageBlob

将图像 URL 转换为 Blob 对象

<div class="buzzts-border">

#### <divider-base /> {#base-urlToImageBlob}

<urlToImageBlob />

<details>
<summary>查看代码</summary>

<<< @/utils/imagex/urlToImageBlob.vue

</details>

#### <divider-param /> {#param-urlToImageBlob}

| 参数属性 | 说明                          | 类型     | 默认值 |
|----------|-------------------------------|----------|--------|
| url      | 要转换的图像 URL              | `string` | 无     |

| 返回值   | 说明                                   |
|----------|----------------------------------------|
| `Promise<Blob>` | 返回 Blob 对象的 Promise          |

#### <divider-desc /> {#desc-urlToImageBlob}

- 通过 Fetch API 获取图像 URL，并将其转换为 Blob 对象

</div>

### urlToImageFile

将图像 URL 转换为 File 对象

<div class="buzzts-border">

#### <divider-base /> {#base-urlToImageFile}

<urlToImageFile />

<details>
<summary>查看代码</summary>

<<< @/utils/imagex/urlToImageFile.vue

</details>

#### <divider-param /> {#param-urlToImageFile}

| 参数属性 | 说明                          | 类型     | 默认值                |
|----------|-------------------------------|----------|-----------------------|
| url      | 要转换的图像 URL              | `string` | 无                    |
| fileName | 文件名（可选）                | `string` | 由 `getImageFileName` 生成 |

| 返回值   | 说明                                   |
|----------|----------------------------------------|
| `Promise<File>` | 返回 File 对象的 Promise          |

#### <divider-desc /> {#desc-urlToImageFile}

- 先将图像 URL 转换为 Blob 对象，然后再转换为 File 对象

</div>

### base64ToImageFile

将 base64 字符串转换为 File 对象

<div class="buzzts-border">

#### <divider-base /> {#base-base64ToImageFile}

<base64ToImageFile />

<details>
<summary>查看代码</summary>

<<< @/utils/imagex/base64ToImageFile.vue

</details>

#### <divider-param /> {#param-base64ToImageFile}

| 参数属性 | 说明                          | 类型     | 默认值                |
|----------|-------------------------------|----------|-----------------------|
| base64   | 要转换的 base64 字符串       | `string` | 无                    |
| fileName | 文件名（可选）                | `string` | 由 `getImageFileName` 生成 |

| 返回值   | 说明                                   |
|----------|----------------------------------------|
| `File`   | 返回转换后的 File 对象                 |

#### <divider-desc /> {#desc-base64ToImageFile}

- 将 base64 字符串解码并转换为 File 对象

</div>

### base64ToImageBlob

将 base64 字符串转换为 Blob 对象

<div class="buzzts-border">

#### <divider-base /> {#base-base64ToImageBlob}

<base64ToImageBlob />

<details>
<summary>查看代码</summary>

<<< @/utils/imagex/base64ToImageBlob.vue

</details>

#### <divider-param /> {#param-base64ToImageBlob}

| 参数属性 | 说明                          | 类型     | 默认值 |
|----------|-------------------------------|----------|--------|
| base64   | 要转换的 base64 字符串       | `string` | 无     |

| 返回值   | 说明                                   |
|----------|----------------------------------------|
| `Blob | null` | 返回 Blob 对象或 null                 |

#### <divider-desc /> {#desc-base64ToImageBlob}

- 将 base64 字符串解码并返回 Blob 对象

</div>

### blobToImageFile

将 Blob 对象转换为 File 对象

<div class="buzzts-border">

#### <divider-base /> {#base-blobToImageFile}

<blobToImageFile />

<details>
<summary>查看代码</summary>

<<< @/utils/imagex/blobToImageFile.vue

</details>

#### <divider-param /> {#param-blobToImageFile}

| 参数属性 | 说明                          | 类型     | 默认值                |
|----------|-------------------------------|----------|-----------------------|
| blob     | 要转换的 Blob 对象            | `Blob`   | 无                    |
| fileName | 文件名（可选）                | `string` | 由 `getImageFileName` 生成 |

| 返回值   | 说明                                   |
|----------|----------------------------------------|
| `File`   | 返回转换后的 File 对象                 |

#### <divider-desc /> {#desc-blobToImageFile}

- 将 Blob 对象转换为 File 对象

</div>

### fileToBase64

将文件对象转换为 base64 字符串

<div class="buzzts-border">

#### <divider-base /> {#base-fileToBase64}

<fileToBase64 />

<details>
<summary>查看代码</summary>

<<< @/utils/imagex/fileToBase64.vue

</details>

#### <divider-param /> {#param-fileToBase64}

| 参数属性 | 说明                          | 类型     | 默认值 |
|----------|-------------------------------|----------|--------|
| file     | 文件对象                      | `File`   | 无     |

| 返回值   | 说明                                   |
|----------|----------------------------------------|
| `Promise<string>` | 返回 Promise 对象，异步处理         |

#### <divider-desc /> {#desc-fileToBase64}

- 使用 FileReader 将文件对象读取为 base64 字符串

</div>