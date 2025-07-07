# search_files

`search_files` 工具可在你的项目工作区内的多个文件中执行正则表达式搜索。为安全起见，它无法搜索当前工作区目录之外的范围。该工具能帮助 Roo 在整个代码库中定位特定的代码模式、文本或其他内容，并提供附带上下文的搜索结果。

---

## 参数

该工具接受以下参数：

- `path` (必需): 相对于当前工作区目录的搜索路径。搜索范围被限制在工作区内。
- `regex` (必需): 用于搜索的正则表达式模式（使用 Rust 正则表达式语法）。
- `file_pattern` (可选): 用于筛选文件的 Glob 模式（例如，`'*.ts'` 用于 TypeScript 文件）。

---

## 功能

此工具使用正则表达式在指定目录中的文件间进行搜索，并显示每个匹配项及其周围的上下文。它就像一个强大的“在文件中查找”功能，可在整个项目结构中运行。

---

## 何时使用？

- 当 Roo 需要查找特定函数或变量的使用位置时。
- 当 Roo 协助重构并需要理解使用模式时。
- 当 Roo 需要定位特定代码模式的所有实例时。
- 当 Roo 需要在多个文件中搜索文本并具备筛选能力时。

---

## 主要特性

- 使用高性能的 Ripgrep 在单个操作中搜索多个文件。
- 显示每个匹配项的上下文（前后各 1 行）。
- 使用 glob 模式按类型筛选文件（例如，仅限 TypeScript 文件）。
- 提供行号以便于参考。
- 使用强大的正则表达式模式进行精确搜索。
- 自动将输出限制为 300 个结果，并附带通知。
- 对超过 500 个字符的行进行截断，并标记为 `"[truncated...]"`。
- 智能地将邻近的匹配项合并为单个块，以提高可读性。

---

## 限制

- 最适用于基于文本的文件（对图像等二进制文件无效）。
- 在处理极大型代码库时，性能可能会下降。
- 使用 Rust 正则表达式语法，可能与其他正则表达式实现略有不同。
- 无法在压缩文件或归档文件中搜索。
- 默认上下文大小是固定的（前后各 1 行）。
- 由于结果分组，当匹配项靠得很近时，可能会显示不同大小的上下文。
- 为安全起见，搜索严格限制在当前工作区内，无法访问父目录或文件系统上的其他位置。

---

## 工作原理

调用 `search_files` 工具时，它会遵循以下流程：

1.  **参数验证**: 验证必需的 `path` 和 `regex` 参数。
2.  **路径解析**: 将相对路径解析为绝对路径。
3.  **执行搜索**:
    -   使用 Ripgrep (rg) 进行高性能文本搜索。
    -   如果指定了文件模式，则应用文件模式筛选。
    -   收集匹配项及其周围的上下文。
4.  **格式化结果**:
    -   使用文件路径、行号和上下文格式化结果。
    -   在每个匹配项前后各显示 1 行上下文。
    -   以易于阅读的方式组织输出结构。
    -   将结果限制为最多 300 个匹配项，并附带通知。
    -   截断超过 500 个字符的行。
    -   将邻近的匹配项合并为连续的块。

---

## 搜索结果格式

搜索结果包括：

- 每个匹配文件的相对文件路径（以 # 为前缀）。
- 每个匹配项前后的上下文行（默认为 1 行）。
- 填充至 3 个空格的行号，后跟 ` | ` 和行内容。
- 每个匹配组后的分隔线 (----)。

示例输出格式：
```
# rel/path/to/app.ts
 11 |   // Some processing logic here
 12 |   // TODO: Implement error handling
 13 |   return processedData;
----

# Showing first 300 of 300+ results. Use a more specific search if necessary.
```

当匹配项彼此靠近时，它们会被合并成一个单独的块，而不是作为独立的结果显示：

```
# rel/path/to/auth.ts
 13 | // Some code here
 14 | // TODO: Add proper validation
 15 | function validateUser(credentials) {
 16 |   // TODO: Implement rate limiting
 17 |   return checkDatabase(credentials);
----
```

---

## 使用场景示例

- 当被要求重构一个函数时，Roo 首先会搜索该函数的所有使用位置，以确保进行全面的更改。
- 在调查错误时，Roo 会搜索相似的模式，以识别整个代码库中的相关问题。
- 在处理技术债务时，Roo 会定位项目中所有的 TODO 注释。
- 在分析依赖项时，Roo 会查找特定模块的所有导入。

---

## 用法示例

在所有 JavaScript 文件中搜索 TODO 注释：
```
<search_files>
<path>src</path>
<regex>TODO|FIXME</regex>
<file_pattern>*.js</file_pattern>
</search_files>
```

查找特定函数的所有用法：
```
<search_files>
<path>.</path>
<regex>function\s+calculateTotal</regex>
<file_pattern>*.{js,ts}</file_pattern>
</search_files>
```

在整个项目中搜索特定的导入模式：
```
<search_files>
<path>.</path>
<regex>import\s+.*\s+from\s+['"]@components/</regex>
</search_files>
