---
sidebar_label: VS Code 语言模型 API
---

# 在 Roo Code 中使用 VS Code 语言模型 API

Roo Code 包含对 [VS Code 语言模型 API](https://code.visualstudio.com/api/extension-guides/language-model) 的*实验性*支持。该 API 允许扩展直接在 VS Code 中提供对语言模型的访问。这意味着您可能可以使用来自以下来源的模型：

*   **GitHub Copilot：** 如果您拥有 Copilot 订阅并已安装该扩展。
*   **其他 VS Code 扩展：** 任何实现语言模型 API 的扩展。

**重要提示：** 此集成为高度实验性功能，可能无法按预期工作。它依赖于其他扩展正确实现 VS Code 语言模型 API。

---

## 先决条件

*   **VS Code：** 语言模型 API 通过 VS Code 提供（Cursor 目前不支持）。
*   **语言模型提供程序扩展：** 您需要一个提供语言模型的扩展。示例包括：
    *   **GitHub Copilot：** 如果您拥有 Copilot 订阅，GitHub Copilot 和 GitHub Copilot Chat 扩展可以提供模型。
    *   **其他扩展：** 在 VS Code 应用市场中搜索提及“Language Model API”或“lm”的扩展。可能还有其他可用的实验性扩展。

---

## 配置

1.  **打开 Roo Code 设置：** 点击 Roo Code 面板中的齿轮图标 (<Codicon name="gear" />)。
2.  **选择提供商：** 从“API 提供商”下拉菜单中选择“VS Code LM API”。
3.  **选择模型：** “语言模型”下拉菜单将（最终）列出可用的模型。格式为 `供应商/系列`。例如，如果您有 Copilot，您可能会看到如下选项：
    *   `copilot - claude-3.5-sonnet`
    *   `copilot - o3-mini`
    *   `copilot - o1-ga`
    *   `copilot - gemini-2.0-flash`

---

## 限制

*   **实验性 API：** VS Code 语言模型 API 仍处于开发阶段。预计会有变化和潜在的不稳定性。
*   **依赖扩展：** 此功能完全依赖于其他扩展提供模型。Roo Code 无法直接控制哪些模型可用。
*   **功能有限：** VS Code 语言模型 API 可能不支持其他 API 提供商的所有功能（例如，图像输入、流式传输、详细使用信息）。
*   **无直接成本控制：** 您需要遵守提供模型的扩展的定价和条款。Roo Code 无法直接跟踪或限制成本。
*   **GitHub Copilot 速率限制：** 当通过 VS Code LM API 使用 GitHub Copilot 时，请注意 GitHub 可能会对 Copilot 的使用施加速率限制。这些限制由 GitHub 控制，而非 Roo Code。


---

## 故障排除

*   **没有模型出现：**
    *   确保您已安装 VS Code。
    *   确保您已安装并启用语言模型提供程序扩展（例如，GitHub Copilot、GitHub Copilot Chat）。
    *   如果使用 Copilot，请确保您已使用您想用的模型发送了一条 Copilot Chat 消息。
*   **意外行为：** 如果遇到意外行为，很可能是底层语言模型 API 或提供程序扩展的问题。请考虑向提供程序扩展的开发者报告问题。
