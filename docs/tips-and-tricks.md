# 提示与技巧

本节收集了一些实用技巧，帮助您更高效地使用 Roo Code。

- 将 Roo Code 拖到[辅助侧边栏](https://code.visualstudio.com/api/ux-guidelines/sidebars#secondary-sidebar)，以便同时查看资源管理器、搜索、源代码管理等。
<img src="/img/right-column-roo.gif" alt="将 Roo 放在右侧栏" width="900" />
- 将 Roo Code 放置在与文件浏览器不同的侧边栏后，您可以将文件（甚至多个文件）从浏览器拖到聊天窗口中。只需在开始拖动文件后按住 Shift 键即可。
- 如果您不使用 [MCP](/features/mcp/overview)，请在 <Codicon name="server" /> MCP 服务器选项卡中将其关闭，以显著减少系统提示的大小。
- 为了让您的[自定义模式](/features/custom-modes)保持专注，请限制它们允许编辑的文件类型。
- 如果您遇到可怕的 `输入长度和最大令牌数超出上下文限制` 错误，您可以通过删除消息、回滚到上一个检查点或临时切换到具有长上下文窗口的模型（如 Gemini）来解决。
- 通常，请仔细考虑您的 `最大令牌数` 设置。您分配给它的每个令牌都会减少用于存储对话历史记录的可用空间。可以考虑仅在“架构师”和“调试”等模式下使用较高的 `最大令牌数` / `最大思考令牌数` 设置，并将“代码”模式的最大令牌数保持在 16k 或更少。
- 如果现实世界中有您希望自定义模式完成的工作的招聘信息，可以尝试让“代码”模式“根据@[url]的招聘信息创建一个自定义模式”。
- 如果您想真正提高效率，可以检出您仓库的多个副本，并在所有副本上并行运行 Roo Code（使用 git 解决任何冲突，就像与人类开发人员一样）。
- 使用“调试”模式时，请让 Roo “在‘调试’模式下启动一个新任务，并提供解决 X 问题所需的所有必要上下文”，这样调试过程将使用其自己的上下文窗口，而不会污染主任务。
- 点击下方的“编辑此页面”，添加您自己的技巧！
- 要管理大文件并减少上下文/资源使用，请调整 `文件读取自动截断阈值` 设置。此设置控制一次性从文件中读取的行数。较低的值可以提高处理非常大文件时的性能，但可能需要更多的读取操作。您可以在 Roo Code 设置的“高级设置”中找到此选项。
- 为 [`roo.acceptInput` 命令](/features/keyboard-shortcuts)设置键盘快捷键，以便在不使用鼠标的情况下接受建议或提交文本输入。这非常适合以键盘为中心的工作流，并能减少手部疲劳。
- 使用**粘性模型**为不同模式分配专门的 AI 模型（例如，规划时使用推理模型，编码时使用非推理模型）。Roo 会自动切换到每个模式上次使用的模型，无需手动选择。
