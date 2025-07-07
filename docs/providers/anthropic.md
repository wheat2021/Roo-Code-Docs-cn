---
sidebar_label: Anthropic
---

# 通过 Roo Code 使用 Anthropic

Anthropic 是一家致力于构建可靠、可解释和可控的人工智能系统的 AI 安全和研究公司。其 Claude 模型以其强大的推理能力、乐于助人和诚实而闻名。

**网站：** [https://www.anthropic.com/](https://www.anthropic.com/)

---

## 获取 API 密钥

1.  **注册/登录：** 前往 [Anthropic 控制台](https://console.anthropic.com/)。创建账户或登录。
2.  **导航至 API 密钥：** 前往 [API 密钥](https://console.anthropic.com/settings/keys) 部分。
3.  **创建密钥：** 点击“创建密钥”。为您的密钥指定一个描述性名称（例如，“Roo Code”）。
4.  **复制密钥：** **重要提示：** 请立即复制 API 密钥。您将无法再次看到它。请妥善保管。

---

## 支持的模型

Roo Code 支持以下 Anthropic Claude 模型：

*   `claude-opus-4-20250514`
*   `claude-opus-4-20250514:thinking` (扩展思考变体)
*   `claude-sonnet-4-20250514` (推荐)
*   `claude-sonnet-4-20250514:thinking` (扩展思考变体)
*   `claude-3-7-sonnet-20250219`
*   `claude-3-7-sonnet-20250219:thinking` (扩展思考变体)
*   `claude-3-5-sonnet-20241022`
*   `claude-3-5-haiku-20241022`
*   `claude-3-opus-20240229`
*   `claude-3-haiku-20240307`

有关每个模型功能的更多详细信息，请参阅 [Anthropic 的模型文档](https://docs.anthropic.com/en/docs/about-claude/models)。

---

## 在 Roo Code 中配置

1.  **打开 Roo Code 设置：** 在 Roo Code 面板中点击齿轮图标 (<Codicon name="gear" />)。
2.  **选择提供商：** 从“API 提供商”下拉菜单中选择“Anthropic”。
3.  **输入 API 密钥：** 将您的 Anthropic API 密钥粘贴到“Anthropic API 密钥”字段中。
4.  **选择模型：** 从“模型”下拉菜单中选择您想要的 Claude 模型。
5.  **（可选）自定义基础 URL：** 如果您需要为 Anthropic API 使用自定义基础 URL，请勾选“使用自定义基础 URL”并输入该 URL。大多数人不需要调整此项。

---

## 提示和说明

*   **提示缓存：** Claude 3 模型支持[提示缓存](https://docs.anthropic.com/en/docs/build-with-claude/prompt-caching)，这可以显著降低重复提示的成本和延迟。
*   **上下文窗口：** Claude 模型拥有较大的上下文窗口（200,000 个令牌），允许您在提示中包含大量代码和上下文。
*   **定价：** 有关最新的定价信息，请参阅 [Anthropic 定价](https://www.anthropic.com/pricing)页面。
*   **速率限制：** Anthropic 根据[使用层级](https://docs.anthropic.com/en/api/rate-limits#requirements-to-advance-tier)设有严格的速率限制。如果您反复达到速率限制，请考虑联系 Anthropic 销售或通过其他提供商（如 [OpenRouter](/providers/openrouter) 或 [Requesty](/providers/requesty)）访问 Claude。
