---
sidebar_label: OpenAI
---

# 通过 Roo Code 使用 OpenAI

Roo Code 支持通过官方 OpenAI API 直接访问模型。

**网站：** [https://openai.com/](https://openai.com/)

---

## 获取 API 密钥

1.  **注册/登录：** 前往 [OpenAI 平台](https://platform.openai.com/)。创建账户或登录。
2.  **导航至 API 密钥：** 前往 [API 密钥](https://platform.openai.com/api-keys) 页面。
3.  **创建密钥：** 点击“Create new secret key”。为你的密钥指定一个描述性名称（例如，“Roo Code”）。
4.  **复制密钥：** **重要提示：** 请*立即*复制 API 密钥。之后你将无法再次查看。请妥善保管。

---

## 支持的模型

Roo Code 支持多种 OpenAI 模型，包括：

*	`o3-mini` (中等推理能力)
*	`o3-mini-high` (高推理能力)
* `o3-mini-low` (低推理能力)
* `o1`
* `o1-preview`
*	`o1-mini`
*   `gpt-4.5-preview`
* `gpt-4o`
* `gpt-4o-mini`

有关最新的模型列表和功能，请参阅 [OpenAI 模型文档](https://platform.openai.com/docs/models)。

---

## 在 Roo Code 中配置

1.  **打开 Roo Code 设置：** 点击 Roo Code 面板中的齿轮图标 (<Codicon name="gear" />)。
2.  **选择提供商：** 从“API Provider”下拉菜单中选择“OpenAI”。
3.  **输入 API 密钥：** 将你的 OpenAI API 密钥粘贴到“OpenAI API Key”字段中。
4.  **选择模型：** 从“Model”下拉菜单中选择你想要的模型。
5.  **（可选）基础 URL：** 如果你需要使用自定义的基础 URL，请输入该 URL。大多数人不需要调整此项。

---

## 提示与说明

*   **定价：** 有关模型成本的详细信息，请参阅 [OpenAI 定价](https://openai.com/pricing) 页面。
*   **Azure OpenAI 服务：** 如果你想使用 Azure OpenAI 服务，请参阅我们关于 [OpenAI 兼容](/providers/openai-compatible) 提供商的部分。
