---
sidebar_label: Unbound
---

# 通过 Roo Code 使用 Unbound

Roo Code 支持通过 [Unbound](https://getunbound.ai/) 访问模型。Unbound 是一个专注于提供安全可靠访问各种大型语言模型 (LLM) 的平台。它充当一个网关，让你可以使用来自 Anthropic 和 OpenAI 等提供商的模型，而无需直接管理多个 API 密钥和配置。Unbound 强调企业使用的安全性和合规性功能。

**网站：** [https://getunbound.ai/](https://getunbound.ai/)

---

## 创建账户

1.  **注册/登录：** 前往 [Unbound 网关](https://gateway.getunbound.ai)。创建账户或登录。
2.  **创建应用程序：** 前往[应用程序](https://gateway.getunbound.ai/ai-gateway-applications)页面，然后点击“创建应用程序”按钮。
3.  **复制 API 密钥：** 将 API 密钥复制到剪贴板。

---

## 支持的模型

Unbound 允许您在应用程序中配置支持的模型列表，Roo Code 将自动从 Unbound API 获取可用模型列表。

---

## 在 Roo Code 中配置

1.  **打开 Roo Code 设置：** 点击 Roo Code 面板中的齿轮图标 (<Codicon name="gear" />)。
2.  **选择提供商：** 从“API 提供商”下拉菜单中选择“Unbound”。
3.  **输入 API 密钥：** 将您的 Unbound API 密钥粘贴到“Unbound API 密钥”字段中。
4.  **选择模型：** 从“模型”下拉菜单中选择您想要的模型。

---

## 提示和说明

*   **注重安全：** Unbound 强调企业使用的安全功能。如果您的组织对 AI 使用有严格的安全要求，Unbound 可能是一个不错的选择。
*   **模型列表刷新：** Roo Code 在设置中专门为 Unbound 提供商提供了一个刷新按钮。这使您可以轻松地从您的 Unbound 应用程序更新可用模型列表，并立即获得关于 API 密钥有效性的反馈。
