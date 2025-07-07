# list_files

`list_files` 工具用于显示指定位置的文件和目录。它能帮助 Roo 理解您的项目结构并有效地在代码库中导航。

---

## 参数

该工具接受以下参数：

- `path` (必需): 要列出其内容的目录路径，相对于当前工作目录。
- `recursive` (可选): 是否递归列出文件。使用 `true` 进行递归列出，`false` 或省略则仅列出顶层内容。

---

## 功能

此工具列出指定位置的所有文件和目录，清晰地展示您的项目结构。它既可以只显示顶层内容，也可以递归地探索子目录。

---

## 使用时机

- 当 Roo 需要理解您的项目结构时
- 当 Roo 在读取特定文件之前，需要探索有哪些可用文件时
- 当 Roo 需要映射代码库以更好地理解其组织结构时
- 在使用像 `read_file` 或 `search_files` 这样更具针对性的工具之前
- 当 Roo 需要在整个项目中检查特定类型的文件（如配置文件）时

---

## 主要特性

- 同时列出文件和目录，并清晰地标记目录
- 提供递归和非递归两种列出模式
- 在递归模式下，智能地忽略常见的超大目录，如 `node_modules` 和 `.git`
- 在递归模式下，遵守 `.gitignore` 规则
- 当 `showRooIgnoredFiles` 启用时，用锁形符号 (🔒) 标记被 `.rooignore` 忽略的文件
- 利用 `ripgrep` 工具优化文件列表性能
- 对结果进行排序，将目录显示在其内容之前，以保持逻辑层次结构
- 以简洁、有条理的格式呈现结果
- 自动在内部建立您项目结构的思维导图

---

## 限制

- 为防止性能问题，文件列表默认上限约为 200 个文件
- 底层的 `ripgrep` 文件列表进程有 10 秒的超时限制；如果超时，可能会返回部分结果。
- 当达到文件数量限制时，会添加一条注释，建议在特定的子目录上使用 `list_files`
- 不适用于确认您刚刚创建的文件是否存在
- 在非常大的目录结构中性能可能会下降
- 出于安全原因，无法列出根目录或主目录中的文件

---

## 工作原理

当调用 `list_files` 工具时，它会遵循以下流程：

1.  **参数验证**: 验证必需的 `path` 参数和可选的 `recursive` 参数。
2.  **路径解析**: 将相对路径解析为绝对路径。
3.  **安全检查**: 防止在根目录或主目录等敏感位置列出文件。
4.  **目录/文件扫描**:
    -   使用 `ripgrep` 工具高效地列出文件，并应用 10 秒超时。
    -   使用 Node.js 的 `fs` 模块列出目录。
    -   对递归和非递归模式应用不同的过滤逻辑。
5.  **结果过滤**:
    -   在递归模式下，跳过常见的超大目录，如 `node_modules`、`.git` 等。
    -   在递归模式下，遵守 `.gitignore` 规则。
    -   处理 `.rooignore` 模式，可以隐藏文件或用锁形符号标记它们。
6.  **格式化**:
    -   用尾部斜杠 (`/`) 标记目录。
    -   对结果进行排序，将目录显示在其内容之前，以保持逻辑层次。
    -   当 `showRooIgnoredFiles` 启用时，用锁形符号 (🔒) 标记被忽略的文件。
    -   默认将结果限制在 200 个文件，并附有关于使用子目录的说明。
    -   为提高可读性而组织结果。

---

## 文件列表格式

文件列表结果包括：

- 每个文件路径单独显示一行
- 目录以尾部斜杠 (`/`) 标记
- 当 `showRooIgnoredFiles` 启用时，被 `.rooignore` 忽略的文件会用锁形符号 (🔒) 标记
- 结果按逻辑排序，目录会出现在其内容之前
- 当达到文件数量限制时，会出现一条消息，建议在特定的子目录上使用 `list_files`

输出格式示例：
```
src/
src/components/
src/components/Button.tsx
src/components/Header.tsx
src/utils/
src/utils/helpers.ts
src/index.ts
...
文件列表已截断 (显示 543 个文件中的 200 个)。请对特定子目录使用 list_files 以获取更多详情。
```

当使用 `.rooignore` 文件且 `showRooIgnoredFiles` 启用时：
```
src/
src/components/
src/components/Button.tsx
src/components/Header.tsx
🔒 src/secrets.json
src/utils/
src/utils/helpers.ts
src/index.ts
```

---

## 使用场景示例

- 开始新任务时，Roo 可能会列出项目文件以了解其结构，然后再深入研究特定代码。
- 当被要求查找特定类型的文件（例如所有 JavaScript 文件）时，Roo 会首先列出目录以确定搜索范围。
- 在提供代码组织建议时，Roo 会首先检查当前的项目结构。
- 在设置新功能时，Roo 会列出相关目录以了解项目的约定。

---

## 用法示例

列出当前目录的顶层文件：
```
<list_files>
<path>.</path>
</list_files>
```

递归列出源目录中的所有文件：
```
<list_files>
<path>src</path>
<recursive>true</recursive>
</list_files>
```

检查特定的项目子目录：
```
<list_files>
<path>src/components</path>
<recursive>false</recursive>
</list_files>
