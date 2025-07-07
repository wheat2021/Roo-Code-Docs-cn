---
sidebar_label: Groq
---

# 通过 Roo Code 使用 Groq

Groq 专注于为大型语言模型提供极高速的推理服务，这得益于其自研的语言处理单元（LPU）。对于支持的模型，这可以显著缩短响应时间。

**网站：** [https://groq.com/](https://groq.com/)

---

## 获取 API 密钥

要通过 Roo Code 使用 Groq，您需要从 [GroqCloud 控制台](https://console.groq.com/) 获取一个 API 密钥。注册或登录后，请转到仪表盘的 API 密钥部分来创建并复制您的密钥。

---

## 支持的模型

Roo Code 会尝试从 Groq API 获取可用模型列表。通过 Groq 提供的常见模型包括：

*   `llama3-8b-8192`
*   `llama3-70b-8192`
*   `mixtral-8x7b-32768`
*   `gemma-7b-it`

有关支持的模型及其功能的最新列表，请参阅 [Groq 文档](https://console.groq.com/docs/models)。

---

## 在 Roo Code 中配置

1.  **打开 Roo Code 设置：** 在 Roo Code 面板中点击齿轮图标 (<Codicon name="gear" />)。
2.  **选择提供商：** 从“API 提供商”下拉菜单中选择“Groq”。
3.  **输入 API 密钥：** 将您的 Groq API 密钥粘贴到“Groq API 密钥”字段中。
4.  **选择模型：** 从“模型”下拉菜单中选择您想要的模型。
