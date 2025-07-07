---
sidebar_label: Mistral AI
---

# 在 Roo Code 中使用 Mistral AI

Roo Code 支持通过 Mistral AI API 访问模型，包括标准的 Mistral 模型和专门用于代码的 Codestral 模型。

**网站：** [https://mistral.ai/](https://mistral.ai/)

---

## 获取 API 密钥

1.  **注册/登录：** 前往 [Mistral 平台](https://console.mistral.ai/)。创建账户或登录。您可能需要完成验证过程。
2.  **创建 API 密钥：**
    - [La Plateforme API 密钥](https://console.mistral.ai/api-keys/) 和/或
    - [Codestral API 密钥](https://console.mistral.ai/codestral)

---

## 支持的模型

Roo Code 支持以下 Mistral 模型：

| 模型 ID                | 模型默认温度 | 函数调用 | 视觉/图像支持 |
|------------------------|-----------------|------------------|--------|
| codestral-latest       | 0.3             | ✅               | ❌      |
| mistral-large-latest   | 0.7             | ✅               | ❌      |
| ministral-8b-latest    | 0.3             | ✅               | ❌      |
| ministral-3b-latest    | 0.3             | ✅               | ❌      |
| mistral-small-latest   | 0.3             | ✅               | ❌      |
| pixtral-large-latest   | 0.7             | ✅               | ✅      |
Roo Code 中的默认模型温度为 0.0，因此您应考虑尝试[调整温度](/features/model-temperature)！

**注意：** 模型可用性和规格可能会发生变化。
请参阅 [Mistral AI 文档](https://docs.mistral.ai/api/)和 [Mistral 模型概述](https://docs.mistral.ai/getting-started/models/models_overview/)获取最新信息。

---

## 在 Roo Code 中配置

1.  **打开 Roo Code 设置：** 在 Roo Code 面板中点击齿轮图标 (<Codicon name="gear" />)。
2.  **选择提供商：** 从“API 提供商”下拉菜单中选择“Mistral”。
3.  **输入 API 密钥：** 如果您使用的是 `mistral` 模型，请将您的 Mistral API 密钥粘贴到“Mistral API 密钥”字段中。如果您打算使用 `codestral-latest`，请参阅下方的“Codestral”部分。
4.  **选择模型：** 从“模型”下拉菜单中选择您想要的模型。

---

## 使用 Codestral

[Codestral](https://docs.mistral.ai/capabilities/code_generation/) 是一个专为代码生成和交互而设计的模型。
仅对于 Codestral，您可以使用不同的端点（默认为 codestral.mistral.ai）。
对于 La Platforme API 密钥，请将 **Codestral 基础 URL** 更改为：https://api.mistral.ai

要使用 Codestral：

1.  **选择“Mistral”作为 API 提供商。**
2.  **选择一个 Codestral 模型**
3.  **输入您的 Codestral (codestral.mistral.ai) 或 La Plateforme (api.mistral.ai) API 密钥。**
