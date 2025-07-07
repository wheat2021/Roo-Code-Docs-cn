# 工具如何工作

Roo Code 使用工具与您的代码和环境进行交互。这些专门的辅助程序执行特定操作，例如读取文件、进行编辑、运行命令或搜索您的代码库。工具为常见的开发任务提供了自动化，无需手动执行。

---

## 工具工作流程

用自然语言描述您想完成的任务，Roo Code 将会：

1.  根据您的请求选择合适的工具
2.  展示工具及其参数供您审查
3.  执行经您批准的工具并显示结果
4.  持续此过程，直到您的任务完成

---

## 工具类别

| 类别 | 用途 | 工具名称 |
| :------- | :------ | :--------- |
| 读取 | 访问文件内容和代码结构 | `read_file`, `search_files`, `list_files`, `list_code_definition_names` |
| 编辑 | 创建或修改文件和代码 | `write_to_file`, `apply_diff` |
| 执行 | 运行命令并执行系统操作 | `execute_command` |
| 浏览器 | 与网页内容交互 | `browser_action` |
| 工作流 | 管理任务流程和上下文 | `ask_followup_question`, `attempt_completion`, `switch_mode`, `new_task` |

---

## 示例：使用工具

以下是典型的工具交互工作方式：

<img src="/img/how-tools-work/how-tools-work.png" alt="工具批准界面，显示“保存”和“拒绝”按钮以及“自动批准”复选框" width="600" />

*工具批准界面显示“保存”/“拒绝”按钮和“自动批准”选项。*

**用户：** 创建一个名为 `greeting.js` 的文件，用于记录一条问候消息

**Roo Code：** （如上图所示，提议使用 `write_to_file` 工具）
```xml
<write_to_file>
<path>greeting.js</path>
<content>
function greet(name) {
  console.log(`Hello, ${name}!`);
}

greet('World');
</content>
<line_count>5</line_count>
</write_to_file>
```

**用户：** （在界面中点击“保存”）

**Roo Code：** （确认文件已创建）

---

## 工具安全与批准


每次使用工具都需要您的明确批准。当 Roo 提议一个工具时，您会看到：

*   一个“保存”按钮，用于批准并执行该工具
*   一个“拒绝”按钮，用于拒绝提议的工具
*   一个可选的“自动批准”设置，用于受信任的操作

这种安全机制确保您能控制哪些文件被修改、哪些命令被执行以及您的代码库如何被更改。在保存工具提议之前，请务必仔细审查。

---

## 核心工具参考

| 工具名称 | 描述 | 类别 |
| :-------- | :---------- | :------- |
| `read_file` | 读取带行号的文件内容 | 读取 |
| `search_files` | 在文件中搜索文本或正则表达式模式 | 读取 |
| `list_files` | 列出指定位置的文件和目录 | 读取 |
| `list_code_definition_names` | 列出类和函数等代码定义 | 读取 |
| `write_to_file` | 创建新文件或覆盖现有文件 | 编辑 |
| `apply_diff` | 对文件的特定部分进行精确更改 | 编辑 |
| `execute_command` | 在 VS Code 终端中运行命令 | 执行 |
| `browser_action` | 在无头浏览器中执行操作 | 浏览器 |
| `ask_followup_question` | 向您提出一个澄清问题 | 工作流 |
| `attempt_completion` | 表示任务已完成 | 工作流 |
| `switch_mode` | 切换到不同的操作模式 | 工作流 |
| `new_task` | 使用特定的起始模式创建一个新的子任务 | 工作流 |

---

## 了解更多关于工具的信息

有关每个工具的更详细信息，包括完整的参数参考和高级用法模式，请参阅[工具使用概览](/advanced-usage/available-tools/tool-use-overview)文档。
