---
sidebar_label: xAI (Grok)
---

# 在 Roo Code 中使用 xAI (Grok)

xAI 是 Grok 背后的公司，Grok 是一款以其对话能力和庞大的上下文窗口而闻名的大型语言模型。Grok 模型旨在提供有帮助、信息丰富且与上下文相关的响应。

**网站：** [https://x.ai/](https://x.ai/)

---

## 获取 API 密钥

1.  **注册/登录：** 前往 [xAI 控制台](https://console.x.ai/)。创建一个账户或登录。
2.  **导航至 API 密钥：** 在您的仪表板中转到 API 密钥部分。
3.  **创建密钥：** 点击创建新的 API 密钥。为您的密钥指定一个描述性名称（例如，“Roo Code”）。
4.  **复制密钥：** **重要提示：** 请立即复制 API 密钥。您将无法再次看到它。请安全地存储它。

---

## 支持的模型

Roo Code 支持以下 xAI Grok 模型：

### Grok-3 模型
* `grok-3-beta` (默认) - xAI 的 Grok-3 beta 模型，具有 131K 上下文窗口
* `grok-3-fast-beta` - xAI 的 Grok-3 fast beta 模型，具有 131K 上下文窗口
* `grok-3-mini-beta` - xAI 的 Grok-3 mini beta 模型，具有 131K 上下文窗口
* `grok-3-mini-fast-beta` - xAI 的 Grok-3 mini fast beta 模型，具有 131K 上下文窗口

### Grok-2 模型
* `grok-2-latest` - xAI 的 Grok-2 模型 - 最新版本，具有 131K 上下文窗口
* `grok-2` - xAI 的 Grok-2 模型，具有 131K 上下文窗口
* `grok-2-1212` - xAI 的 Grok-2 模型 (版本 1212)，具有 131K 上下文窗口

### Grok 视觉模型
* `grok-2-vision-latest` - xAI 的 Grok-2 视觉模型 - 最新版本，支持图像，具有 32K 上下文窗口
* `grok-2-vision` - xAI 的 Grok-2 视觉模型，支持图像，具有 32K 上下文窗口
* `grok-2-vision-1212` - xAI 的 Grok-2 视觉模型 (版本 1212)，支持图像，具有 32K 上下文窗口
* `grok-vision-beta` - xAI 的 Grok Vision Beta 模型，支持图像，具有 8K 上下文窗口

### 旧版模型
* `grok-beta` - xAI 的 Grok Beta 模型 (旧版)，具有 131K 上下文窗口

---

## 在 Roo Code 中配置

1.  **打开 Roo Code 设置：** 点击 Roo Code 面板中的齿轮图标 (<Codicon name="gear" />)。
2.  **选择提供商：** 从“API 提供商”下拉菜单中选择“xAI”。
3.  **输入 API 密钥：** 将您的 xAI API 密钥粘贴到“xAI API 密钥”字段中。
4.  **选择模型：** 从“模型”下拉菜单中选择您想要的 Grok 模型。

---

## 推理能力

Grok 3 Mini 模型具有专门的推理能力，使其能够“先思考再回答”——这对于解决复杂问题特别有用。

### 支持推理的模型

推理功能仅受以下模型支持：
* `grok-3-mini-beta`
* `grok-3-mini-fast-beta`

Grok 3 模型 `grok-3-beta` 和 `grok-3-fast-beta` 不支持推理。

### 控制推理强度

使用支持推理的模型时，您可以通过 `reasoning_effort` 参数来控制模型的思考强度：

* `low`：最少的思考时间，使用较少的 token 以获得快速响应
* `high`：最长的思考时间，利用更多的 token 来解决复杂问题

对于应快速完成的简单查询，请选择 `low`；对于响应延迟不那么重要的难题，请选择 `high`。

### 主要特点

* **分步解决问题**：模型在给出答案前会系统地思考问题
* **数学与量化能力**：在数值挑战和逻辑谜题方面表现出色
* **访问推理轨迹**：可通过响应完成对象中的 `reasoning_content` 字段访问模型的思考过程

---

## 提示和说明

* **上下文窗口：** 大多数 Grok 模型都具有庞大的上下文窗口（高达 131K token），允许您在提示中包含大量代码和上下文。
* **视觉能力：** 当您需要处理或分析图像时，请选择支持视觉的模型（`grok-2-vision-latest`、`grok-2-vision` 等）。
* **定价：** 定价因模型而异，输入成本从每百万 token 0.3 美元到 5.0 美元不等，输出成本从每百万 token 0.5 美元到 25.0 美元不等。请参阅 xAI 文档以获取最新的定价信息。
* **性能权衡：** “Fast”变体通常提供更快的响应时间，但成本可能更高；而“mini”变体更经济，但能力可能有所降低。