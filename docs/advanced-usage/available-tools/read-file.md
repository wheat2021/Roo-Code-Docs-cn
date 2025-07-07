# read_file

`read_file` 工具用于检查项目中的文件内容。它允许 Roo 理解代码、配置文件和文档，以提供更好的帮助。

:::info 多文件支持
当启用[并发文件读取](/features/concurrent-file-reads)实验性功能时，此工具可以使用增强的 XML 参数格式同时读取多个文件。这显著提高了需要分析多个相关文件的任务的效率。
:::

---

## 参数

该工具根据您的配置接受两种格式的参数：

### 标准格式（单文件）

- `path` (必需): 要读取的文件的路径，相对于当前工作目录。
- `start_line` (可选): 开始读取的行号（从 1 开始）。
- `end_line` (可选): 结束读取的行号（从 1 开始，包含此行）。

:::note 旧版格式
虽然为了向后兼容仍然支持单文件参数（`path`、`start_line`、`end_line`），但我们建议使用新的 `args` 格式以保持一致性和未来的兼容性。
:::

### 增强格式（多文件 - 实验性）

当启用[并发文件读取](/features/concurrent-file-reads)时，该工具接受一个包含多个文件条目的 `args` 参数：

- `args` (必需): 多个文件规范的容器。
  - `file` (必需): 单个文件规范。
    - `path` (必需): 要读取的文件的路径。
    - `line_range` (可选): 行范围规范（例如，"1-50" 或 "100-150"）。

---

## 功能

此工具读取指定文件的内容，并返回带行号的内容以便参考。它可以读取整个文件或特定部分，甚至可以从 PDF 和 Word 文档中提取文本。

---

## 使用时机

- 当 Roo 需要理解现有代码结构时。
- 当 Roo 需要分析配置文件时。
- 当 Roo 需要从文本文件中提取信息时。
- 当 Roo 在建议更改前需要查看代码时。
- 当需要在讨论中引用特定行号时。

---

## 主要特性

- 显示带行号的文件内容，便于参考。
- 可通过指定行范围读取文件的特定部分。
- 从 PDF 和 DOCX 文件中提取可读文本。
- 未指定行范围时，自动截断大型文本文件，并显示文件开头部分。
- 为被截断的大型代码文件提供带行范围的方法摘要。
- 高效地仅流式传输请求的行范围，以获得更好的性能。
- 通过行号轻松讨论代码的特定部分。
- **多文件支持** (实验性): 通过批量批准同时读取多个文件。

---

## 多文件功能 (实验性)

当启用[并发文件读取](/features/concurrent-file-reads)实验性功能时，`read_file` 工具将获得增强功能：

### 批量处理
- 单次请求最多可读取 100 个文件（可配置，默认为 15）。
- 并行处理以提高性能。
- 用户同意的批量批准界面。

### 增强的用户体验
- 针对多个文件的单一批准对话框。
- 单个文件的覆盖选项。
- 清晰地显示将要访问的文件。
- 优雅地处理混合成功/失败的情况。

### 提高效率
- 减少多个批准对话框带来的中断。
- 通过并行文件读取加快处理速度。
- 智能批处理相关文件。
- 可配置的并发限制以匹配系统能力。

---

## 限制

- 如果不使用行范围参数，可能无法高效处理超大文件。
- 对于二进制文件（PDF 和 DOCX 除外），可能返回非人类可读的内容。
- **多文件模式**: 需要启用实验性功能，并且可能存在稳定性问题。

---

## 工作原理

当调用 `read_file` 工具时，它会遵循以下流程：

1.  **参数验证**: 验证必需的 `path` 参数和可选参数。
2.  **路径解析**: 将相对路径解析为绝对路径。
3.  **读取策略选择**:
    - 该工具使用严格的优先级层次结构（详见下文）。
    - 它在范围读取、自动截断或完整文件读取之间进行选择。
4.  **内容处理**:
    - 为内容添加行号（例如，"1 | const x = 13"），其中 `1 |` 是行号。
    - 对于被截断的文件，添加截断通知和方法定义。
    - 对于特殊格式（PDF, DOCX），提取可读文本。

---

## 读取策略优先级

该工具使用明确的决策层次结构来确定如何读取文件：

1.  **第一优先级：显式行范围**
    - 如果提供了 `start_line` 或 `end_line`，工具总是执行范围读取。
    - 该实现高效地仅流式传输请求的行，使其适用于处理大文件。
    - 这优先于所有其他选项。

2.  **第二优先级：大型文本文件的自动截断**
    - 仅当**所有**以下条件都满足时适用：
      - 未指定 `start_line` 或 `end_line`。
      - 文件被识别为基于文本的文件（不是像 PDF/DOCX 这样的二进制文件）。
      - 文件的总行数超过 `maxReadFileLine` 设置（默认为 500 行）。
    - 当发生自动截断时：
      - 工具只读取*前* `maxReadFileLine` 行。
      - 它会附加一个表示截断的通知（例如，`[仅显示 1200 行中的 500 行...]`）。
      - 对于代码文件，它可能还会附加在截断部分内找到的源代码定义的摘要。
    - **特殊情况 - 仅定义模式**: 当 `maxReadFileLine` 设置为 `0` 时，该工具仅返回源代码定义，不包含任何文件内容。

3.  **默认行为：读取整个文件**
    - 如果既未给出显式范围，也未应用自动截断（例如，文件在行数限制内，或者是支持的二进制类型），工具将读取整个内容。
    - 对于像 PDF 和 DOCX 这样的支持格式，它会尝试提取完整的文本内容。

---

## 使用示例

- 当被要求解释或改进代码时，Roo 首先读取相关文件以了解当前实现。
- 在排查配置问题时，Roo 读取配置文件以识别潜在问题。
- 在处理文档时，Roo 在建议改进前会阅读现有文档以了解当前内容。

---

## 用法示例

以下是几个演示如何使用 `read_file` 工具以及您可能收到的典型输出的场景。

### 读取整个文件

要读取文件的完整内容：

**输入:**
```xml
<read_file>
<path>src/app.js</path>
</read_file>
```

**模拟输出 (对于像 `example_small.txt` 这样的小文件):**
```
1 | This is the first line.
2 | This is the second line.
3 | This is the third line.
```
*(输出将根据实际文件内容而变化)*

### 读取特定行

只读取特定范围的行（例如，46-68）：

**输入:**
```xml
<read_file>
<path>src/app.js</path>
<start_line>46</start_line>
<end_line>68</end_line>
</read_file>
```

**模拟输出 (对于 `example_five_lines.txt` 的第 2-3 行):**
```
2 | Content of line two.
3 | Content of line three.
```
*(输出仅显示请求的行及其原始行号)*

### 读取大型文本文件（自动截断）

在未指定行范围的情况下读取大型文本文件时，如果内容超过内部行数限制（例如 500 行），工具会自动截断内容。

**输入:**
```xml
<read_file>
<path>logs/large_app.log</path>
</read_file>
```

**模拟输出 (对于一个有 1500 行日志文件，限制为 500 行):**
```
1 | Log entry 1...
2 | Log entry 2...
...
500 | Log entry 500...

[仅显示 1500 行中的 500 行。使用 start_line 和 end_line 读取特定范围。]
// 可选：对于代码文件，源代码定义摘要可能会出现在这里
```
*(输出显示开头的行，直到 `maxReadFileLine` 限制，并附有截断通知。使用行范围以获得完整访问权限。)*

### 仅读取定义

当用户设置中 `maxReadFileLine` 设置为 `0` 时，该工具仅返回源代码定义，不返回文件内容：

**输入:**
```xml
<!-- 假设用户设置中 maxReadFileLine 设置为 0 -->
<read_file>
<path>src/services/auth.service.ts</path>
</read_file>
```

**模拟输出:**
```xml
<file>
  <path>src/services/auth.service.ts</path>
  <list_code_definition_names>
    class AuthService
      method validateUser
      method generateToken
  </list_code_definition_names>
  <notice>仅显示 150 行中的 0 行。使用 start_line 和 end_line 读取特定范围。</notice>
</file>
```
*(此模式提供了文件结构的快速概览，而无需读取内容。)*

### 尝试读取不存在的文件

如果指定的文件不存在：

**输入:**
```xml
<read_file>
<path>non_existent_file.txt</path>
</read_file>
```

**模拟输出 (错误):**
```
错误：在路径 'non_existent_file.txt' 未找到文件。
```

### 尝试读取被阻止的文件

如果文件被 `.rooignore` 文件中的规则排除：

**输入:**
```xml
<read_file>
<path>.env</path>
</read_file>
```

**模拟输出 (错误):**
```
错误：被 .rooignore 规则拒绝访问
```

---

## 多文件示例 (实验性)

当启用[并发文件读取](/features/concurrent-file-reads)实验性功能时，您可以使用增强的 XML 格式同时读取多个文件。

### 读取多个完整文件

要一次读取多个完整文件：

**输入:**
```xml
<read_file>
<args>
  <file>
    <path>src/app.ts</path>
  </file>
  <file>
    <path>src/utils.ts</path>
  </file>
  <file>
    <path>src/config.json</path>
  </file>
</args>
</read_file>
```

**模拟输出:**
```xml
<files>
  <file>
    <path>src/app.ts</path>
    <content>
      1 | import React from 'react'
      2 | import { Utils } from './utils'
      3 | // ... 文件其余内容
    </content>
  </file>
  <file>
    <path>src/utils.ts</path>
    <content>
      1 | export class Utils {
      2 |   static formatDate(date: Date): string {
      3 |     // ... 工具函数
    </content>
  </file>
  <file>
    <path>src/config.json</path>
    <content>
      1 | {
      2 |   "apiUrl": "https://api.example.com",
      3 |   "timeout": 5000
      4 | }
    </content>
  </file>
</files>
```

### 从多个文件读取特定行范围

要从多个文件读取特定部分：

**输入:**
```xml
<read_file>
<args>
  <file>
    <path>src/app.ts</path>
    <line_range>1-20</line_range>
    <line_range>45-60</line_range>
  </file>
  <file>
    <path>src/utils.ts</path>
    <line_range>10-25</line_range>
  </file>
</args>
</read_file>
```

**模拟输出:**
```xml
<files>
  <file>
    <path>src/app.ts</path>
    <content>
      1 | import React from 'react'
      2 | import { Utils } from './utils'
      ...
      20 | const App = () => {
      
      45 |   const handleSubmit = () => {
      46 |     // 处理表单提交
      ...
      60 |   }
    </content>
  </file>
  <file>
    <path>src/utils.ts</path>
    <content>
      10 |   static formatDate(date: Date): string {
      11 |     return date.toISOString().split('T')[0]
      ...
      25 |   }
    </content>
  </file>
</files>
```

### 处理混合结果（部分文件被拒绝/阻止）

当某些文件被批准而其他文件被拒绝或阻止时：

**输入:**
```xml
<read_file>
<args>
  <file>
    <path>src/app.ts</path>
  </file>
  <file>
    <path>.env</path>
  </file>
  <file>
    <path>src/secret-config.ts</path>
  </file>
</args>
</read_file>
```

**模拟输出:**
```xml
<files>
  <file>
    <path>src/app.ts</path>
    <content>
      1 | import React from 'react'
      2 | // ... 文件内容成功读取
    </content>
  </file>
  <file>
    <path>.env</path>
    <error>被 .rooignore 规则拒绝访问</error>
  </file>
  <file>
    <path>src/secret-config.ts</path>
    <error>用户拒绝访问文件</error>
  </file>
</files>
```

### 批量批准界面

当请求多个文件时，您会看到一个批量批准界面，允许您：

- **全部批准**: 授予对所有请求文件的访问权限。
- **全部拒绝**: 拒绝所有请求文件的访问权限。
- **单独控制**: 覆盖特定文件的决定。
- **文件预览**: 单击文件头在编辑器中打开它们。

该界面清晰地显示每个文件路径，使您在授予权限前能轻松了解 Roo 想要访问的内容。

---

## 向后兼容性

增强的多文件格式完全向后兼容。使用 `path` 参数的现有单文件请求将继续像以前一样工作，无论实验性功能是否启用。
