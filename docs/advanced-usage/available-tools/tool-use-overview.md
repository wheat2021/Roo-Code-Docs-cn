# 工具使用概览

Roo Code 实现了一个复杂的工具系统，允许 AI 模型以受控且安全的方式与您的开发环境进行交互。本文档解释了工具的工作原理、调用时机以及管理方式。

---

## 核心概念

### 工具组

工具根据其功能被组织成逻辑组：

| 类别 | 目的 | 工具 | 常见用途 |
|---|---|---|---|
| **读取组** | 文件系统读取和探索 | [read_file](/advanced-usage/available-tools/read-file)、[list_files](/advanced-usage/available-tools/list-files)、[list_code_definition_names](/advanced-usage/available-tools/list-code-definition-names) | 代码探索和分析 |
| **搜索组** | 模式和语义搜索 | [search_files](/advanced-usage/available-tools/search-files)、[codebase_search](/advanced-usage/available-tools/codebase-search) | 查找代码模式和功能 |
| **编辑组** | 文件系统修改 | [apply_diff](/advanced-usage/available-tools/apply-diff)、[insert_content](/advanced-usage/available-tools/insert-content)、[search_and_replace](/advanced-usage/available-tools/search-and-replace)、[write_to_file](/advanced-usage/available-tools/write-to-file) | 代码更改和文件操作 |
| **浏览器组** | Web 自动化 | [browser_action](/advanced-usage/available-tools/browser-action) | Web 测试和交互 |
| **命令组** | 系统命令执行 | [execute_command](/advanced-usage/available-tools/execute-command) | 运行脚本、构建项目 |
| **MCP 组** | 外部工具集成 | [use_mcp_tool](/advanced-usage/available-tools/use-mcp-tool)、[access_mcp_resource](/advanced-usage/available-tools/access-mcp-resource) | 通过外部服务器实现专门功能 |
| **工作流组** | 模式和任务管理 | [switch_mode](/advanced-usage/available-tools/switch-mode)、[new_task](/advanced-usage/available-tools/new-task)、[ask_followup_question](/advanced-usage/available-tools/ask-followup-question)、[attempt_completion](/advanced-usage/available-tools/attempt-completion) | 上下文切换和任务组织 |

### 始终可用的工具

无论当前处于何种模式，某些工具始终可用：

- [ask_followup_question](/advanced-usage/available-tools/ask-followup-question)：从用户处收集额外信息
- [attempt_completion](/advanced-usage/available-tools/attempt-completion)：标志任务完成
- [switch_mode](/advanced-usage/available-tools/switch-mode)：更改操作模式
- [new_task](/advanced-usage/available-tools/new-task)：创建子任务

---

## 可用工具

### 读取工具
这些工具帮助 Roo 理解您的代码和项目：

- [read_file](/advanced-usage/available-tools/read-file) - 检查文件内容
- [list_files](/advanced-usage/available-tools/list-files) - 映射您项目的文件结构
- [list_code_definition_names](/advanced-usage/available-tools/list-code-definition-names) - 创建您代码的结构图

### 搜索工具
这些工具帮助 Roo 在您的代码库中查找模式和功能：

- [search_files](/advanced-usage/available-tools/search-files) - 使用正则表达式跨多个文件查找模式
- [codebase_search](/advanced-usage/available-tools/codebase-search) - 在您已索引的代码库中执行语义搜索

### 编辑工具
这些工具帮助 Roo 对您的代码进行更改：

- [apply_diff](/advanced-usage/available-tools/apply-diff) - 对您的代码进行精确、外科手术式的更改
- [insert_content](/advanced-usage/available-tools/insert-content) - 添加新内容行而不修改现有行
- [search_and_replace](/advanced-usage/available-tools/search-and-replace) - 在文件中查找并替换文本或正则表达式模式
- [write_to_file](/advanced-usage/available-tools/write-to-file) - 创建新文件或完全重写现有文件

### 浏览器工具
这些工具帮助 Roo 与 Web 应用程序交互：

- [browser_action](/advanced-usage/available-tools/browser-action) - 自动化浏览器交互

### 命令工具
这些工具帮助 Roo 执行命令：

- [execute_command](/advanced-usage/available-tools/execute-command) - 运行系统命令和程序

### MCP 工具
这些工具帮助 Roo 连接外部服务：

- [use_mcp_tool](/advanced-usage/available-tools/use-mcp-tool) - 使用专门的外部工具
- [access_mcp_resource](/advanced-usage/available-tools/access-mcp-resource) - 访问外部数据源

### 工作流工具
这些工具帮助管理对话和任务流程：

- [ask_followup_question](/advanced-usage/available-tools/ask-followup-question) - 从您那里获取额外信息
- [attempt_completion](/advanced-usage/available-tools/attempt-completion) - 呈现最终结果
- [switch_mode](/advanced-usage/available-tools/switch-mode) - 切换到不同模式以执行专门任务
- [new_task](/advanced-usage/available-tools/new-task) - 创建新的子任务

---

## 工具调用机制

### 处理复杂任务

对于某些需要多个步骤的复杂操作，Roo 不仅仅是即时想出解决方案。相反，它遵循预定义的内部计划以确保一致性和准确性。

一个典型的例子是创建一个新的 MCP 服务器，其内部标识为 `create_mcp_server`。**此标识符不代表您会看到的被调用的工具。** 相反，当您要求 Roo 创建一个服务器时，它会触发这个已知的、多步骤的工作流。

这个特定的工作流由 Roo 使用其内部的 `fetch_instructions` 工具（任务为 `create_mcp_server`）来启动，以检索详细的计划。然后，该计划指导 Roo 按顺序调用几个标准的、有文档记录的工具，例如：

*   [`execute_command`](/advanced-usage/available-tools/execute-command) 用于运行设置脚本（例如 `npx @modelcontextprotocol/create-server`）。
*   [`write_to_file`](/advanced-usage/available-tools/write-to-file) 或 [`apply_diff`](/advanced-usage/available-tools/apply-diff) 用于创建或修改服务器代码和配置文件。
*   [`ask_followup_question`](/advanced-usage/available-tools/ask-followup-question) 用于从您那里收集必要的信息，如 API 密钥。
*   根据需要使用其他标准工具，以完成确定文件位置或更新配置条目等步骤。

因此，虽然整个任务（如 `create_mcp_server`）很复杂，但最终是通过智能地编排您环境中可用的标准工具来完成的。这种方法使 Roo 能够通过利用此处记录的工具来可靠地执行复杂操作。

### 工具调用时机

工具在特定条件下被调用：

1.  **直接任务需求**
    *   当 LLM 决定需要特定操作来完成任务时
    *   响应用户请求时
    *   在自动化工作流期间

2.  **基于模式的可用性**
    *   不同的模式启用不同的工具集
    *   模式切换可以触发工具可用性的变化
    *   某些工具仅限于特定模式

3.  **依赖上下文的调用**
    *   基于工作区的当前状态
    *   响应系统事件时
    *   在错误处理和恢复期间

### 决策过程

系统使用一个多步骤过程来确定工具的可用性：

1.  **模式验证**
    ```typescript
    isToolAllowedForMode(
        tool: string,
        modeSlug: string,
        customModes: ModeConfig[],
        toolRequirements?: Record<string, boolean>,
        toolParams?: Record<string, any>
    )
    ```

2.  **需求检查**
    *   系统能力验证
    *   资源可用性
    *   权限验证

3.  **参数验证**
    *   必需参数的存在性
    *   参数类型检查
    *   值验证

---

## 技术实现

### 工具调用处理

1.  **初始化**
    *   验证工具名称和参数
    *   检查模式兼容性
    *   验证需求

2.  **执行**
    ```typescript
    const toolCall = {
        type: "tool_call",
        name: chunk.name,
        arguments: chunk.input,
        callId: chunk.callId
    }
    ```

3.  **结果处理**
    *   成功/失败判定
    *   结果格式化
    *   错误处理

### 安全与权限

1.  **访问控制**
    *   文件系统限制
    *   命令执行限制
    *   网络访问控制

2.  **验证层**
    *   特定于工具的验证
    *   基于模式的限制
    *   系统级检查

---

## 模式集成

### 基于模式的工具访问

工具的可用性基于当前模式：

- **代码模式**：完全访问文件系统工具、代码编辑能力、命令执行
- **提问模式**：仅限于读取工具、信息收集能力，无文件系统修改
- **架构师模式**：专注于设计的工具、文档能力、有限的执行权限
- **自定义模式**：可以配置特定的工具访问权限以用于专门的工作流

### 模式切换

1.  **过程**
    *   保存当前模式状态
    *   更新工具可用性
    *   上下文切换

2.  **对工具的影响**
    *   工具集变更
    *   权限调整
    *   上下文保留

---

## 最佳实践

### 工具使用指南

1.  **效率**
    *   为任务使用最具体的工具
    *   避免冗余的工具调用
    *   尽可能批量操作

2.  **安全**
    *   在工具调用前验证输入
    *   使用最低所需权限
    *   遵循安全最佳实践

3.  **错误处理**
    *   实现适当的错误检查
    *   提供有意义的错误消息
    *   优雅地处理失败

### 常见模式

1.  **信息收集**
    ```
    [ask_followup_question](/advanced-usage/available-tools/ask-followup-question) → [read_file](/advanced-usage/available-tools/read-file) → [codebase_search](/advanced-usage/available-tools/codebase-search)
    ```

2.  **代码修改**
    ```
    [read_file](/advanced-usage/available-tools/read-file) → [apply_diff](/advanced-usage/available-tools/apply-diff) → [attempt_completion](/advanced-usage/available-tools/attempt-completion)
    ```

3.  **任务管理**
    ```
    [new_task](/advanced-usage/available-tools/new-task) → [switch_mode](/advanced-usage/available-tools/switch-mode) → [execute_command](/advanced-usage/available-tools/execute-command)
    ```

---

## 错误处理与恢复

### 错误类型

1.  **特定于工具的错误**
    *   参数验证失败
    *   执行错误
    *   资源访问问题

2.  **系统错误**
    *   权限被拒绝
    *   资源不可用
    *   网络故障

3.  **上下文错误**
    *   工具的无效模式
    *   缺少需求
    *   状态不一致

### 恢复策略

1.  **自动恢复**
    *   重试机制
    *   回退选项
    *   状态恢复

2.  **用户干预**
    *   错误通知
    *   恢复建议
    *   手动干预选项
