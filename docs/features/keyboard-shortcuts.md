---
sidebar_label: 键盘导航
---

# 键盘导航

Roo Code 界面支持键盘导航和快捷键，以简化您的工作流程并减少对鼠标交互的依赖。

---

## 可用的键盘命令

Roo Code 提供键盘命令来增强您的工作流程。本页重点介绍 `roo.acceptInput` 命令，但这里是所有键盘命令的快速参考：

| 命令 | 描述 | 默认快捷键 |
|---|---|---|
| `roo.acceptInput` | 提交文本或接受主要建议 | 无（可配置） |
| `roo.focus` | 聚焦 Roo 输入框 | 无（可配置） |
| 向上/向下箭头 | 浏览提示历史记录 | 内置 |

### 键盘命令的主要优点

* **键盘驱动界面**：无需鼠标交互即可提交文本或选择主要建议按钮
* **提高可访问性**：对于有行动不便或使用鼠标感到不适的用户至关重要
* **Vim/Neovim 兼容性**：为来自以键盘为中心的环境的开发人员提供无缝过渡
* **工作流程效率**：减少开发任务期间在键盘和鼠标之间的上下文切换

---

## roo.acceptInput 命令

`roo.acceptInput` 命令允许您使用键盘快捷键提交文本或接受建议，而无需在输入区域单击按钮或按 Enter 键。

### 功能说明

`roo.acceptInput` 命令是一个通用的输入提交命令。触发时，它会：

- 在文本输入区域时提交您当前的文本或图像输入（相当于按 Enter 键）
- 当操作按钮可见时（例如确认/取消按钮或任何其他操作按钮），单击主要（第一个）按钮

### 详细设置指南

#### 方法一：使用 VS Code 用户界面

1. 打开命令面板（在 Mac 上为 `Ctrl+Shift+P` 或 `Cmd+Shift+P`）
2. 输入“首选项：打开键盘快捷方式”
3. 在搜索框中，输入“roo.acceptInput”
4. 在结果中找到“Roo: 接受输入/建议”
5. 单击命令左侧的 + 图标
6. 按下您想要的组合键（例如 `Ctrl+Enter` 或 `Alt+Enter`）
7. 按 Enter 键确认

#### 方法二：直接编辑 keybindings.json

1. 打开命令面板（在 Mac 上为 `Ctrl+Shift+P` 或 `Cmd+Shift+P`）
2. 输入“首选项：打开键盘快捷方式 (JSON)”
3. 将以下条目添加到 JSON 数组中：

```json
{
  "key": "ctrl+enter",  // 或您偏好的组合键
  "command": "roo.acceptInput",
  "when": "rooViewFocused"  // 这是一个上下文条件，确保该命令仅在 Roo 获得焦点时有效
}
```

您也可以使用更具体的条件：
```json
{
  "key": "ctrl+enter",
  "command": "roo.acceptInput",
  "when": "webviewViewFocus && webviewViewId == 'roo-cline.SidebarProvider'"
}
```

#### 推荐的组合键

选择一个不与现有 VS Code 快捷键冲突的组合键：

- `Alt+Enter` - 输入时易于按下
- `Ctrl+Space` - 熟悉自动完成功能的用户会很习惯
- `Ctrl+Enter` - 直观的命令执行方式
- `Alt+A` - “Accept”（接受）的助记符

### 实际用例

#### 快速开发工作流程

- **文本提交**：无需将手从键盘上移开即可向 Roo 发送消息
- **操作确认**：接受保存文件、运行命令或应用差异等操作
- **多步骤流程**：快速完成需要确认或输入的步骤
- **连续任务**：以最小的中断将多个任务链接在一起

#### 以键盘为中心的开发

- **Vim/Neovim 工作流程**：如果您来自 Vim/Neovim 背景，可以保持以键盘为中心的工作流程
- **IDE 集成**：与其他 VS Code 键盘快捷键一起使用，获得无缝体验
- **代码审查**：在使用 Roo 审查代码时快速接受建议
- **文档编写**：在生成文档时提交文本并接受格式建议

#### 可访问性用例

- **手部行动不便**：对于使用鼠标有困难的用户至关重要
- **预防重复性劳损**：减少鼠标使用以预防或管理重复性劳损
- **屏幕阅读器集成**：与屏幕阅读器配合良好，适用于视障用户
- **语音控制兼容性**：在使用语音控制软件时，可通过语音命令触发

### 可访问性优势

`roo.acceptInput` 命令在设计时考虑了可访问性：

- **减少对鼠标的依赖**：无需伸手去拿鼠标即可完成整个工作流程
- **减轻身体压力**：帮助因使用鼠标而感到不适或疼痛的用户
- **替代输入法**：支持依赖键盘导航的行动不便的用户
- **工作流程优化**：对于来自 Vim/Neovim 等以键盘为中心的环境的用户尤其有价值

### 以键盘为中心的工作流程

以下是一些完整的工作流程示例，展示了如何有效地将键盘快捷键与 Roo 结合使用：

#### 开发工作流程示例

1. 打开 VS Code 并导航到您的项目
2. 通过侧边栏打开 Roo
3. 输入您的请求：“为用户注册创建一个 REST API 端点”
4. 当 Roo 询问框架偏好时，使用您的 `roo.acceptInput` 快捷键选择第一个建议
5. 继续使用快捷键接受代码生成建议
6. 当 Roo 提议保存文件时，再次使用快捷键确认
7. 使用 VS Code 的内置快捷键在创建的文件中导航

#### 代码审查工作流程

1. 选择您要审查的代码，并使用 VS Code 的“复制”命令
2. 要求 Roo 审查它：“审查此代码是否存在安全问题”
3. 当 Roo 询问有关代码上下文的澄清问题时，使用您的快捷键接受建议
4. 当 Roo 提供改进建议时，再次使用快捷键接受实施建议

### 故障排除

| 问题 | 解决方案 |
|---|---|
| 快捷键不起作用 | 确保 Roo 已获得焦点（首先单击 Roo 面板） |
| 选择了错误的建议 | 该命令总是选择第一个（主要）按钮；如果您需要其他选项，请使用鼠标 |
| 与现有快捷键冲突 | 在 VS Code 键盘设置中尝试不同的组合键 |
| 使用时没有视觉反馈 | 这是正常的 - 该命令会静默激活功能，没有视觉确认 |
| 快捷键工作不一致 | 确保 `when` 子句在您的 keybindings.json 中配置正确（`rooViewFocused` 或特定于 webview 的条件） |

### 技术实现

`roo.acceptInput` 命令的实现如下：

- 命令注册为 `roo.acceptInput`，在命令面板中显示标题为“Roo: 接受输入/建议”
- 触发时，它会向活动的 Roo webview 发送一条“acceptInput”消息
- webview 根据当前的 UI 状态确定适当的操作：
  - 如果操作按钮可见且已启用，则单击主要操作按钮
  - 如果文本区域已启用且包含文本/图像，则发送消息
- 没有默认键绑定 - 用户可以分配自己偏好的快捷键

### 限制

- 仅在 Roo 界面处于活动状态时有效
- 如果当前没有可用的输入或建议，则无效
- 当显示多个选项时，优先选择主要（第一个）按钮

---

## 命令行风格的提示历史导航

使用箭头键以类似终端的体验浏览您的提示历史记录。此功能使您可以轻松地重用和优化以前的提示，无论是来自当前对话还是过去的任务。

### 主要功能
- **上/下箭头**：循环浏览以前的提示。
- **上下文感知**：在对话和任务历史记录之间切换。
- **保留输入**：记住您正在输入的内容。

### 为何如此重要

**之前**：重用提示意味着向上滚动、复制和粘贴。
- 繁琐且缓慢
- 容易迷失方向
- 中断您的工作流程

**有了提示历史导航**：无需离开键盘即可快速访问过去的提示。

### 工作原理

导航的设计直观，并能适应您当前的上下文。

#### 在活动对话中
- **向上箭头**：显示您发送的最后一个提示。继续按可返回更早的对话。
- **向下箭头**：在对话历史记录中向前移动，最终返回到您正在输入的文本。

#### 开始新聊天
- **向上箭头**：显示当前工作区中任务历史记录中最新的提示。
- **向下箭头**：在任务历史记录中向前移动。

#### 边缘情况
- 如果您在导航时开始输入，历史记录将被清除，并保留您的新文本。
- 导航仅在光标位于输入框的第一行或最后一行时有效，以避免干扰多行编辑。

### 配置

此功能默认启用。没有需要配置的设置。

### 优点

- **更快的工作流程**：无需使用鼠标即可重用提示。
- **更好的上下文**：轻松访问并基于以前的交互进行构建。
- **更少的中断**：专注于手头的任务。

### 常见问题

**“为什么我按向上箭头时没有任何反应？”**
- 您可能正处于多行提示的中间。光标必须在第一行。
- 当前上下文可能没有可用的历史记录。

**“对话历史记录和任务历史记录有什么区别？”**
- **对话历史记录** 包括您当前活动聊天会话中的提示。
- **任务历史记录** 包括您当前工作区中所有先前任务的初始提示。