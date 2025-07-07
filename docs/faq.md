import KangarooIcon from '@site/src/components/KangarooIcon';

# 常见问题解答

本页面回答一些关于 Roo Code 的常见问题。

---

## 常规问题

### 什么是 Roo Code？

Roo Code 是一款内嵌于您编辑器中的 AI 驱动的自主编码代理。

### Roo Code 是如何工作的？

Roo Code 使用大型语言模型 (LLM) 来理解您的请求并将其转化为行动。它可以：

*   读写您项目中的文件。
*   在您的 VS Code 终端中执行命令。
*   进行网页浏览（如果启用）。
*   通过模型上下文协议 (MCP) 使用外部工具。

您通过一个聊天界面与 Roo Code 互动，在其中提供指令并审查/批准其建议的操作。

### Roo Code 能做什么？

Roo Code 可以帮助完成各种编码任务，包括：

*   根据自然语言描述生成代码。
*   重构现有代码。
*   修复错误。
*   编写文档。
*   解释代码。
*   回答关于您代码库的问题。
*   自动化重复性任务。
*   创建新文件和项目。

### Roo Code 是免费的吗？

Roo Code 扩展本身是免费且开源的。然而，Roo Code 依赖外部 API 提供商（如 [Anthropic](providers/anthropic)、[OpenAI](providers/openai)、[OpenRouter](providers/openrouter)、[Requesty](providers/requesty) 等）来实现其 AI 功能。这些提供商通常根据处理的令牌数量收取 API 使用费。您需要创建一个账户并从您选择的提供商那里获取 API 密钥。详情请参阅[设置您的第一个 AI 提供商](/getting-started/connecting-api-provider)。

### 使用 Roo Code 有哪些风险？

Roo Code 是一个强大的工具，负责任地使用它非常重要。以下是一些需要注意的事项：

*   **Roo Code 可能会犯错。** 在批准 Roo Code 提出的更改之前，请务必仔细审查。
*   **Roo Code 可以执行命令。** 在允许 Roo Code 运行命令时要非常谨慎，尤其是在使用自动批准功能时。
*   **Roo Code 可以访问互联网。** 如果您使用的提供商支持网页浏览，请注意 Roo Code 可能会访问敏感信息。

---

## 设置与安装

### 如何安装 Roo Code？

请参阅[安装指南](/getting-started/installing)获取详细说明。

### 支持哪些 API 提供商？

Roo Code 支持多种 API 提供商，包括：
*   [Anthropic (Claude)](/providers/anthropic)
*   [OpenAI](/providers/openai)
*   [OpenRouter](/providers/openrouter)
*   [Google Gemini](/providers/gemini)
*   [Glama](/providers/glama)
*   [AWS Bedrock](/providers/bedrock)
*   [GCP Vertex AI](/providers/vertex)
*   [Ollama](/providers/ollama)
*   [LM Studio](/providers/lmstudio)
*   [DeepSeek](/providers/deepseek)
*   [Mistral](/providers/mistral)
*   [Unbound](/providers/unbound)
*   [Requesty](/providers/requesty)
*   [VS Code 语言模型 API](/providers/vscode-lm)

### 如何获取 API 密钥？
每个 API 提供商都有其自己获取 API 密钥的流程。请参阅[设置您的第一个 AI 提供商](/getting-started/connecting-api-provider)以获取每个提供商相关文档的链接。

### 我可以使用本地模型运行 Roo Code 吗？
是的，Roo Code 支持使用 [Ollama](/providers/ollama) 和 [LM Studio](/providers/lmstudio) 在本地运行模型。请参阅[使用本地模型](/advanced-usage/local-models)获取说明。

---

## 使用方法

### 如何开始一个新任务？
打开 Roo Code 面板 (<KangarooIcon />) 并在聊天框中输入您的任务。请清晰具体地说明您希望 Roo Code 做什么。最佳实践请参阅[输入您的请求](/basic-usage/typing-your-requests)。

### Roo Code 中的模式是什么？
[模式](/basic-usage/using-modes)是 Roo Code 可以扮演的不同角色，每个角色都有特定的重点和能力集。内置的模式有：

*   **代码 (Code)：** 用于通用编码任务。
*   **架构师 (Architect)：** 用于规划和技术领导。
*   **提问 (Ask)：** 用于回答问题和提供信息。
*   **调试 (Debug)：** 用于系统性问题诊断。
您还可以创建[自定义模式](/features/custom-modes)。

### 如何在模式之间切换？

使用聊天输入区的下拉菜单选择不同的模式，或使用 `/` 命令切换到特定模式。

### 什么是工具？如何使用它们？
[工具](/basic-usage/how-tools-work)是 Roo Code 与您的系统交互的方式。Roo Code 会自动选择并使用适当的工具来完成您的任务。您无需直接调用工具。系统会提示您批准或拒绝每次工具使用。

### 什么是上下文提及？
[上下文提及](/basic-usage/context-mentions)是一种向 Roo Code 提供关于您项目的特定信息的方式，例如文件、文件夹或问题。使用“@”符号后跟您想提及的项目（例如，`@/src/file.ts`、`@problems`）。

### Roo Code 可以访问互联网吗？

是的，如果您使用的提供商的模型支持网页浏览。请注意允许此操作的安全隐患。

### Roo Code 可以在我的终端中运行命令吗？

是的，Roo Code 可以在您的 VS Code 终端中执行命令。除非您为命令启用了自动批准，否则在执行每个命令之前都会提示您批准。在自动批准命令时要极其谨慎。如果您在终端命令方面遇到问题，请参阅[Shell 集成指南](/features/shell-integration)进行故障排除。

### 如何向 Roo Code 提供反馈？

您可以通过批准或拒绝 Roo Code 提出的操作来提供反馈。您可以使用反馈字段提供额外的反馈。

### 我可以自定义 Roo Code 的行为吗？

是的，您可以通过多种方式自定义 Roo Code：

*   **自定义指令：** 提供适用于所有模式的通用指令，或特定于模式的指令。
*   **自定义模式：** 创建具有量身定制的提示和一些工具权限的您自己的模式。
*   **`.roorules` 文件：** 在您的项目中创建 `.roorules` 文件以提供额外的指导方针。
*   **设置：** 调整各种设置，例如自动批准、差异编辑等。

### Roo Code 有任何自动批准设置吗？
是的，Roo Code 有一些设置，启用后会自动批准操作。在此处了解更多信息[此处](/features/auto-approving-actions)。

---

## 高级功能

### 我可以离线使用 Roo 吗？
是的，如果您使用[本地模型](/advanced-usage/local-models)。

### 什么是 MCP (模型上下文协议)？
[MCP](/features/mcp/overview) 是一个允许 Roo Code 与外部服务器通信的协议，通过自定义工具和资源扩展其功能。

### 我可以创建自己的 MCP 服务器吗？

是的，您可以创建自己的 MCP 服务器以向 Roo Code 添加自定义功能。详情请参阅 [MCP 文档](https://github.com/modelcontextprotocol)。

### 什么是代码库索引？

[代码库索引](/features/experimental/codebase-indexing)是一项实验性功能，它使用 AI 嵌入为您的项目创建一个语义搜索索引。这使得 Roo Code 能够通过基于含义而不仅仅是关键字查找相关代码，从而更好地理解和导航大型代码库。

### 代码库索引的成本是多少？

代码库索引需要一个 OpenAI API 密钥来生成嵌入，以及一个 Qdrant 向量数据库用于存储。成本取决于您的项目大小和使用的嵌入模型。初始索引是最昂贵的部分；后续更新是增量的，成本要低得多。

---

## 故障排除

### Roo Code 没有响应。我该怎么办？

*   确保您的 API 密钥正确且未过期。
*   检查您的互联网连接。
*   检查您选择的 API 提供商的状态。
*   尝试重启 VS Code。
*   如果问题仍然存在，请在 [GitHub](https://github.com/RooCodeInc/Roo-Code/issues) 或 [Discord](https://discord.gg/roocode) 上报告问题。

### 我看到了一个错误消息。这是什么意思？

错误消息应提供有关问题的一些信息。如果您不确定如何解决，请在 [Discord](https://discord.gg/roocode) 中寻求帮助。

### Roo Code 做了我不想做的更改。如何撤销它们？

Roo Code 使用 VS Code 的内置文件编辑功能。您可以使用标准的“撤销”命令 (Ctrl/Cmd + Z) 来恢复更改。此外，如果启用了实验性的检查点功能，Roo 可以恢复对文件所做的更改。

### Roo Code 无法写入 markdown 文件。出了什么问题？

如果 Roo Code 无法写入 `.md` 文件并出现“无法打开差异编辑器”或“write_to_file 工具失败”等错误，这通常是由干扰文件编辑的 VS Code 扩展或设置引起的：

**常见原因：**
- 具有“保存时格式化”功能的扩展
- 默认以预览模式打开 markdown 文件的 VS Code 设置
- Markdown 预览扩展或类似的 markdown 处理扩展

**解决方案：**
- 禁用任何在保存时自动格式化文件的扩展
- 从您的 VS Code `settings.json` 中删除这些设置：
  ```json
  "markdown.preview.openMarkdownLinks": "inPreview",
  "workbench.editorAssociations": {
    "*.md": "vscode.markdown.preview.editor"
  }
  ```
- 暂时禁用与 markdown 相关的扩展，以测试它们是否是问题的原因
- 做出这些更改后重启 VS Code

### 如何报告错误或建议功能？

请在 Roo Code 的 [问题页面](https://github.com/RooCodeInc/Roo-Code/issues) 和 [功能请求页面](https://github.com/RooCodeInc/Roo-Code/discussions/categories/feature-requests?discussions_q=is%3Aopen+category%3A%22Feature+Requests%22+sort%3Atop) 上报告错误或建议功能。
