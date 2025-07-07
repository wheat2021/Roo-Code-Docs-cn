---
sidebar_label: OpenRouter
---

# 通过 Roo Code 使用 OpenRouter

OpenRouter 是一个 AI 平台，它通过单一的 API 提供了对来自不同提供商的各种语言模型的访问。这可以简化设置，并让你轻松地试验不同的模型。

**网站：** [https://openrouter.ai/](https://openrouter.ai/)

---

## 获取 API 密钥

1.  **注册/登录：** 前往 [OpenRouter 网站](https://openrouter.ai/)。使用你的 Google 或 GitHub 帐户登录。
2.  **获取 API 密钥：** 前往 [密钥页面](https://openrouter.ai/keys)。你应该会看到一个列出的 API 密钥。如果没有，请创建一个新密钥。
3.  **复制密钥：** 复制该 API 密钥。

---

## 支持的模型

OpenRouter 支持大量且不断增加的模型。Roo Code 会自动获取可用模型的列表。请参阅 [OpenRouter 模型页面](https://openrouter.ai/models) 获取完整且最新的列表。

---

## 在 Roo Code 中配置

1.  **打开 Roo Code 设置：** 点击 Roo Code 面板中的齿轮图标 (<Codicon name="gear" />)。
2.  **选择提供商：** 从“API 提供商”下拉菜单中选择“OpenRouter”。
3.  **输入 API 密钥：** 将你的 OpenRouter API 密钥粘贴到“OpenRouter API 密钥”字段中。
4.  **选择模型：** 从“模型”下拉菜单中选择你想要的模型。
5.  **（可选）自定义基础 URL：** 如果你需要为 OpenRouter API 使用自定义的基础 URL，请勾选“使用自定义基础 URL”并输入该 URL。大多数用户可以留空此项。

---

## 支持的转换

OpenRouter 提供了一个[可选的“中间删减”消息转换功能](https://openrouter.ai/docs/features/message-transforms)，以帮助处理超出模型最大上下文大小的提示。你可以通过勾选“将提示和消息链压缩至上下文大小”框来启用它。

---

## 提示和说明

*   **模型选择：** OpenRouter 提供了广泛的模型选择。请进行试验，找到最适合你需求的模型。
*   **定价：** OpenRouter 根据底层模型的定价收费。详情请参阅 [OpenRouter 模型页面](https://openrouter.ai/models)。
*   **提示缓存：**
    *   OpenRouter 会将缓存请求传递给支持它的底层模型。请查看 [OpenRouter 模型页面](https://openrouter.ai/models) 以了解哪些模型提供缓存功能。
    *   对于大多数模型，如果模型本身支持缓存（类似于 Requesty 的工作方式），缓存功能应会自动激活。
    *   **通过 OpenRouter 使用 Gemini 模型的例外情况：** 由于通过 OpenRouter 访问时，有时会观察到 Google 的缓存机制存在潜在的响应延迟，因此*专门针对 Gemini 模型*需要一个手动激活步骤。
    *   如果通过 OpenRouter 使用 **Gemini 模型**，你**必须手动勾选**提供商设置中的“启用提示缓存”框以激活该模型的缓存功能。此复选框是一个临时解决方案。对于 OpenRouter 上的非 Gemini 模型，此复选框对于缓存不是必需的。
*   **自带密钥 (BYOK)：** 如果你为底层服务使用自己的密钥，OpenRouter 会收取其正常费用的 5%。Roo Code 会自动调整成本计算以反映这一点。
