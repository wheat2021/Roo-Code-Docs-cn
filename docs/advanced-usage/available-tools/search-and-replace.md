# search_and_replace

`search_and_replace` 工具用于在文件中查找和替换文本，同时支持文字字符串和正则表达式模式。它允许在多个位置进行有针对性的替换，并可选择在特定的行范围内操作。

---

## 参数

### 必需参数

- `path`: 要修改的文件的相对路径（从工作区根目录开始）。
- `search`: 要查找的文本字符串或正则表达式模式。
- `replace`: 用于替换匹配项的文本。

### 可选参数

- `start_line`: 搜索范围开始的行号（从 1 开始）。
- `end_line`: 搜索范围结束的行号（包含此行）。
- `use_regex`: 设置为 `"true"` 以将 `search` 参数视为正则表达式模式（默认为 `false`）。
- `ignore_case`: 设置为 `"true"` 以执行不区分大小写的搜索（默认为 `false`）。

---

## 功能说明

该工具读取指定的文件，并根据提供的参数执行搜索和替换操作。它可以对整个文件进行操作，也可以限制在特定的行范围内。更改会以差异（diff）视图的形式呈现，供用户在保存前审查和批准。

---

## 使用场景

- 在文件中重命名变量、函数或类时。
- 需要统一更新特定的文本字符串或值时。
- 使用正则表达式应用模式化更改时。
- 代码重构需要替换特定模式时。
- 在文件的特定区域内进行有针对性的更改时。

---

## 主要特性

- **灵活搜索**: 支持文字文本和正则表达式模式。
- **大小写控制**: 可选择在搜索时忽略大小写。
- **范围替换**: 可以将替换限制在特定的行范围内（`start_line`、`end_line`）。
- **全局替换**: 默认在整个文件（或指定范围）内执行替换。
- **交互式批准**: 在差异（diff）视图中显示建议的更改，供用户审查和批准。
- **支持用户编辑**: 允许在差异（diff）视图中直接编辑建议的内容。
- **上下文跟踪**: 记录文件编辑操作。
- **错误处理**: 检查缺失的参数、文件访问问题和无效的行号。

---

## 限制

- **单文件操作**: 一次只能对一个文件进行操作。若要跨多个文件查找模式，请先使用 `search_files`。
- **审查开销**: 强制性的差异（diff）视图批准增加了一个交互步骤。
- **正则表达式复杂性**: 复杂的正则表达式模式可能需要仔细构建和测试。

---

## 工作原理

调用 `search_and_replace` 工具时，它会遵循以下流程：

1.  **参数验证**: 检查必需的 `path`、`search`、`replace` 参数，并验证行号和布尔标志等可选参数。
2.  **文件读取**: 读取 `path` 指定的目标文件的内容。
3.  **正则表达式构建**:
    *   如果 `use_regex` 为 `false`，则对 `search` 字符串进行转义，以将其视为文字文本。
    *   创建一个带有 `g`（全局）标志和可选的 `i`（忽略大小写）标志的 `RegExp` 对象。
4.  **执行替换**:
    *   如果提供了 `start_line` 或 `end_line`，则将文件内容拆分为行，隔离相关部分，在该部分执行替换，然后重新构建文件内容。
    *   如果未指定行范围，则对整个文件内容字符串执行替换。
5.  **差异（Diff）视图交互**:
    *   在差异（diff）视图中打开文件，显示原始内容与建议内容的对比。
    *   使用替换结果更新差异（diff）视图。
6.  **用户批准**: 通过 `askApproval` 提交更改。如果被拒绝，则恢复原状。
7.  **保存更改**: 如果获得批准，则保存更改（包括在差异视图中所做的任何用户编辑）。
8.  **文件上下文跟踪**: 使用 `cline.getFileContextTracker().trackFileContext` 跟踪编辑。
9.  **结果报告**: 向 AI 模型报告成功（包括用户编辑）或失败。

---

## 使用示例

在整个文件中进行简单的文本替换：

```xml
<search_and_replace>
<path>src/config.js</path>
<search>API_KEY_OLD</search>
<replace>API_KEY_NEW</replace>
</search_and_replace>
```

不区分大小写的正则表达式替换，以更新函数调用：

```xml
<search_and_replace>
<path>src/app.ts</path>
<search>processData\((.*?)\)</search>
<replace>handleData($1)</replace>
<use_regex>true</use_regex>
<ignore_case>true</ignore_case>
</search_and_replace>
```

仅在第 10 到 20 行之间替换文本：

```xml
<search_and_replace>
<path>README.md</path>
<search>Draft</search>
<replace>Final</replace>
<start_line>10</start_line>
<end_line>20</end_line>
</search_and_replace>