---
sidebar_label: .rooignore
---

# 使用 .rooignore 控制文件访问

`.rooignore` 文件是管理 Roo Code 与项目文件交互的一项关键功能。它允许您指定 Roo 不应访问或修改的文件和目录，其工作方式类似于 Git 的 `.gitignore`。

---

## 什么是 `.rooignore`？

*   **目的**：保护敏感信息，防止意外更改构建产物或大型资源，并从整体上定义 Roo 在您工作区内的操作范围。
*   **如何使用**：在 VS Code 工作区的根目录中创建一个名为 `.rooignore` 的文件。在此文件中列出模式，以告知 Roo 哪些文件和目录应被忽略。
*   **范围**：`.rooignore` 同时影响 Roo 的工具和上下文提及（如 `@directory` 附件）。

Roo 会主动监控 `.rooignore` 文件。您所做的任何更改都会自动重新加载，确保 Roo 始终使用最新的规则。`.rooignore` 文件本身始终被隐式忽略，因此 Roo 无法更改自己的访问规则。

---

## 模式语法

`.rooignore` 的语法与 `.gitignore` 完全相同。以下是常见示例：

*   `node_modules/`：忽略整个 `node_modules` 目录。
*   `*.log`：忽略所有以 `.log` 结尾的文件。
*   `config/secrets.json`：忽略一个特定文件。
*   `!important.log`：一个例外情况；即使存在像 `*.log` 这样更广泛的模式，Roo 也*不会*忽略这个特定文件。
*   `build/`：忽略 `build` 目录。
*   `docs/**/*.md`：忽略 `docs` 目录及其子目录中的所有 Markdown 文件。

有关语法的全面指南，请参阅 [关于 .gitignore 的官方 Git 文档](https://git-scm.com/docs/gitignore)。

---

## Roo 工具如何与 `.rooignore` 交互

`.rooignore` 规则在各种 Roo 工具中强制执行：

### 严格执行（读取和写入）

这些工具在执行任何文件操作之前会直接检查 `.rooignore`。如果文件被忽略，操作将被阻止：

*   [`read_file`](/advanced-usage/available-tools/read-file)：不会读取被忽略的文件。
*   [`write_to_file`](/advanced-usage/available-tools/write-to-file)：不会写入或创建新的被忽略的文件。
*   [`apply_diff`](/advanced-usage/available-tools/apply-diff)：不会对被忽略的文件应用差异。
*   [`insert_content`](/advanced-usage/available-tools/insert-content)：不会写入被忽略的文件。
*   [`search_and_replace`](/advanced-usage/available-tools/search-and-replace)：不会在被忽略的文件内进行搜索和替换。
*   [`list_code_definition_names`](/advanced-usage/available-tools/list-code-definition-names)：不会解析被忽略的文件以获取代码符号。

### 文件发现和列出

*   **[`list_files`](/advanced-usage/available-tools/list-files) 工具和 `@directory` 附件**：当 Roo 列出文件或您使用 `@directory` 附件时，被忽略的文件会被省略或标记为 🔒 符号（请参阅下文的“用户体验”）。两者使用相同的过滤逻辑。
*   **环境详情**：提供给 Roo 的关于您工作区的信息（如打开的标签页和项目结构）会经过筛选，以排除或标记被忽略的项目。

### 上下文提及

*   **`@directory` 附件**：目录内容遵循 `.rooignore` 模式。根据 `showRooIgnoredFiles` 设置，被忽略的文件会被过滤掉或标记为 `[🔒]` 前缀。
*   **单个文件提及**：被忽略的文件会返回“(文件已被 .rooignore 忽略)”而不是其内容。

### 命令执行

*   **[`execute_command`](/advanced-usage/available-tools/execute-command) 工具**：此工具会检查命令（来自预定义列表，如 `cat` 或 `grep`）是否指向一个被忽略的文件。如果是，则阻止执行。

---

## 主要限制和范围

*   **以工作区为中心**：`.rooignore` 规则**仅适用于当前 VS Code 工作区根目录内的文件和目录**。此范围之外的文件不受影响。
*   **[`execute_command`](/advanced-usage/available-tools/execute-command) 的特殊性**：对 `execute_command` 的保护仅限于预定义的文件读取命令列表。自定义脚本或不常见的实用程序可能不会被捕获。
*   **并非完全沙盒**：`.rooignore` 是一个通过其工具控制 Roo 文件访问的强大工具，但它不会创建系统级的沙盒。

---

## 用户体验和通知

*   **视觉提示 (🔒)**：在文件列表和 `@directory` 附件中，被 `.rooignore` 忽略的文件可能会被标记为锁形符号 (🔒)，具体取决于 `showRooIgnoredFiles` 设置（默认为 `true`）。
*   **忽略消息**：单个文件提及会返回“(文件已被 .rooignore 忽略)”而不是其内容。
*   **错误消息**：如果工具操作被阻止，Roo 会收到一个错误：`“对 [file_path] 的访问已被 .rooignore 文件设置阻止。您必须尝试在不使用此文件的情况下继续任务，或请求用户更新 .rooignore 文件。”`
*   **聊天通知**：当某个操作因 `.rooignore` 而被阻止时，您通常会在 Roo 聊天界面中看到一条通知。

本指南帮助您了解 `.rooignore` 功能、其能力和当前限制，以便您能有效地管理 Roo 与您代码库的交互。
