# 增强提示

Roo Code 中的“增强提示”功能可帮助您在将提示发送给 AI 模型之前提高其质量和有效性。通过单击聊天输入框中的 <Codicon name="sparkle" /> 图标，您可以自动优化初始请求，使其更清晰、更具体，从而更有可能产生预期的结果。

---

## 为什么要使用增强提示？

*   **提高清晰度：** Roo Code 可以重新组织您的提示，使其更易于 AI 模型理解。
*   **添加上下文：** 增强过程可以为您的提示添加相关上下文，例如当前文件路径或所选代码。
*   **更好的指令：** Roo Code 可以添加指令来引导 AI 给出更有帮助的响应（例如，要求特定的格式或详细程度）。
*   **减少歧义：** “增强提示”有助于消除歧义，并确保 Roo Code 理解您的意图。
*   **一致性：** Roo 将始终以相同的方式向 AI 格式化提示。

---

## 如何使用增强提示

1.  **输入您的初始提示：** 像往常一样，在 Roo Code 聊天输入框中输入您的请求。这可以是一个简单的问题、一个复杂的任务描述，或介于两者之间的任何内容。
2.  **单击 <Codicon name="sparkle" /> 图标：** 不要按 Enter 键，而是单击位于聊天输入框右下角的 <Codicon name="sparkle" /> 图标。
3.  **查看增强后的提示：** Roo Code 会将您的原始提示替换为增强版本。请查看增强后的提示，确保它准确反映了您的意图。您可以在发送前进一步优化增强后的提示。
4.  **发送增强后的提示：** 按 Enter 键或单击发送图标 (<Codicon name="send" />) 将增强后的提示发送给 Roo Code。

---

## 自定义增强过程

“增强提示”功能使用可自定义的提示模板。您可以修改此模板，以根据您的特定需求定制增强过程。

1.  **打开“提示”选项卡：** 单击 Roo Code 顶部菜单栏中的 <Codicon name="notebook" /> 图标。
2.  **选择“ENHANCE”选项卡：** 您应该会看到列出的支持提示，包括“ENHANCE”。单击此选项卡。
3.  **编辑提示模板：** 修改“提示”字段中的文本。

默认提示模板包含占位符 `${userInput}`，它将被您的原始提示替换。您可以修改它以适应模型的提示格式，并指示它如何增强您的请求。

---

## API 配置

默认情况下，用于“增强提示”的 API 配置与为 Roo Code 任务选择的配置相同，但可以更改：

1.  **打开“提示”选项卡：** 单击 Roo Code 顶部菜单栏中的 <Codicon name="notebook" /> 图标。
2.  **选择“ENHANCE”选项卡：** 您应该会看到一个“API 配置”下拉菜单。
3.  **选择一个 API 配置：** 选择一个现有配置，未来的“增强提示”请求将被发送到该配置的提供商/模型。

---

## 限制和最佳实践

*   **实验性功能：** 提示增强是一项实验性功能。增强后提示的质量可能会因您请求的复杂性和底层模型的能力而异。
*   **仔细审查：** 在发送增强后的提示之前，请务必仔细审查。Roo Code 可能会做出不符合您意图的更改。
*   **迭代过程：** 您可以多次使用“增强提示”功能来迭代优化您的提示。
*   **不能替代清晰的指令：** 虽然“增强提示”可以提供帮助，但从一开始就编写清晰、具体的提示仍然很重要。

通过使用“增强提示”功能，您可以提高与 Roo Code 交互的质量，并获得更准确、更有帮助的响应。
