---
sidebar_label: Claude Code
---

# Claude Code 提供商

Claude Code 提供商允许您通过其官方 CLI（命令行界面）而不是 Web API 来使用 Anthropic 的 Claude 模型。这使您可以直接从 Roo Code 访问您的 Claude Max 订阅。

:::info 设置说明
在使用 Claude Code 提供商之前，请确保您已完成以下步骤：

1.  **安装 Claude CLI**：从 [Anthropic 的文档](https://docs.anthropic.com/en/docs/claude-code/setup) 下载并安装官方命令行工具。
2.  **验证**：在您的终端中运行 `claude` 来启动应用程序。应用程序运行后，输入 `/login` 登录您的 Anthropic 帐户。此步骤是授予 Roo Code 访问您的 Claude 订阅所必需的。
3.  **验证设置**：通过运行 `claude --version` 确认 CLI 是否正常工作。这可以确保 Roo Code 能够找到并使用该可执行文件。
4.  **在 Roo Code 中配置**：
    *   转到 Roo Code 设置并选择 **"Claude Code"** 作为您的 API 提供商。
    *   如果您将 CLI 安装在自定义位置，请将 **"Claude Code Path"** 设置为完整的可执行文件路径（例如，`/usr/local/bin/claude`）。否则，您可以将其留空。
    *   从可用选项列表中选择您想要的模型。

配置完成后，Roo Code 将使用您本地的 Claude CLI 安装与 Anthropic 的模型进行交互，并利用您现有的订阅。
:::


:::warning 环境变量使用
`claude` 命令行工具与其他 Anthropic SDK 一样，可以使用 `ANTHROPIC_API_KEY` 环境变量进行身份验证。这是在非交互式环境中授权 CLI 工具的常用方法。

如果您的系统上设置了此环境变量，`claude` 工具可能会使用它进行身份验证，而不是使用交互式的 `/login` 方法。当 Roo Code 执行该工具时，它将准确反映正在使用 API 密钥，因为这是 `claude` CLI 本身的底层行为。
:::

**网站：** [https://docs.anthropic.com/en/docs/claude-code/setup](https://docs.anthropic.com/en/docs/claude-code/setup)

---

## 主要特性
- **直接 CLI 访问**：使用 Anthropic 的官方 Claude CLI 工具进行模型交互。
- **高级推理**：完全支持 Claude 的思考模式和推理能力。
- **成本透明**：显示 CLI 报告的精确使用成本。
- **灵活配置**：与您现有的 Claude CLI 设置配合使用。

---

## 为何使用此提供商

- **无需 API 密钥**：使用您现有的 Claude CLI 身份验证。
- **成本优势**：利用 CLI 订阅费率和透明的成本报告。
- **最新功能**：在 CLI 中发布新功能时即可访问。
- **高级推理**：完全支持 Claude 的思考模式。

## 工作原理

Claude Code 提供商的工作原理如下：

1. **运行命令**：使用您的提示执行 `claude` CLI 命令。
2. **处理输出**：通过高级解析分块处理 CLI 的 JSON 输出。
3. **处理推理**：在可用时捕获并显示 Claude 的思考过程。
4. **跟踪使用情况**：报告 CLI 提供的令牌使用量和成本。

该提供商与 Roo Code 的界面集成，让您在底层使用 Claude CLI 的同时，获得与其他提供商相同的使用体验。

---

## 配置

您只需要配置一个可选设置：

### **Claude Code 路径**
- **设置**：`claudeCodePath`
- **描述**：您的 Claude CLI 可执行文件的路径。
- **默认值**：`claude`（假定它在您的系统 PATH 中）。
- **何时更改**：如果您将 Claude CLI 安装在自定义位置。

**自定义路径示例：**
- macOS/Linux: `/usr/local/bin/claude` 或 `~/bin/claude`

---

## 支持的模型

Claude Code 提供商支持以下 Claude 模型：

- **Claude Sonnet 4**（最新，推荐）
- **Claude Opus 4**（功能最强）
- **Claude 3.7 Sonnet**
- **Claude 3.5 Sonnet**
- **Claude 3.5 Haiku**（响应速度快）

具体可用的模型取决于您的 Claude CLI 订阅和计划。


---


## 常见问题

**“我需要为此提供商提供 Claude API 密钥吗？”**
- 通常不需要。您可以在 `claude` 应用程序中使用 `/login` 命令进行交互式身份验证。
- 但是，如果设置了 `ANTHROPIC_API_KEY` 环境变量，Claude CLI 可能会使用它进行身份验证。有关详细信息，请参阅上面的警告。

**“如何安装 Claude CLI？”**
- 请访问 [Anthropic 的 CLI 文档](https://docs.anthropic.com/en/docs/claude-code/setup) 获取安装说明
- CLI 会自行处理身份验证和设置

**“我为什么要使用这个提供商而不是常规的 Anthropic 提供商？”**
- 根据您的订阅，可能会有潜在的成本优势

**“如果 CLI 不在我的 PATH 中怎么办？”**
- 在 Claude Code 路径设置中设置自定义路径
- 指向您安装 CLI 的完整路径
