---
sidebar_label: 你的第一个任务
---
import KangarooIcon from '@site/src/components/KangarooIcon';

# 使用 Roo Code 开始你的第一个任务

现在你已经[配置了你的 AI 提供商和模型](/getting-started/connecting-api-provider)，可以开始使用 Roo Code 了！本指南将引导你完成第一次互动。

---

## 第一步：打开 Roo Code 面板

点击 VS Code 活动栏（窗口侧边的垂直栏）中的 Roo Code 图标 (<KangarooIcon />) 来打开聊天界面。如果你没有看到该图标，请确认扩展已安装并启用。

<img src="/img/your-first-task/your-first-task.png" alt="Roo Code icon in VS Code Activity Bar" width="800" />

*活动栏中的 Roo Code 图标可以打开聊天界面。*

---

## 第二步：输入你的任务

在面板底部的聊天框中，输入一个清晰、简洁的描述，告诉 Roo Code 你想做什么。一些有效的任务示例：

*   “创建一个名为 `hello.txt` 的文件，内容为‘Hello, world!’。”
*   “编写一个 Python 函数，将两个数字相加。”
*   “创建一个 HTML 文件，用于一个简单的网站，标题为‘Roo test’”

不需要特殊的命令或语法——只需使用自然语言。

<img src="/img/your-first-task/your-first-task-6.png" alt="Typing a task in the Roo Code chat interface" width="500" />
*用自然语言输入你的任务 - 无需特殊语法。*

---

## 第三步：发送你的任务

按 Enter 键或点击输入框右侧的发送图标 (<Codicon name="send" />)。

---

## 第四步：审查并批准操作

Roo Code 会分析你的请求并提出具体的操作建议。这些操作可能包括：

*   **读取文件：** 显示它需要访问的文件内容
*   **写入文件：** 显示带有建议更改的差异对比（增加的行显示为绿色，删除的行显示为红色）
*   **执行命令：** 显示将在你的终端中运行的确切命令
*   **使用浏览器：** 概述浏览器操作（点击、输入等）
*   **提出问题：** 在需要时请求澄清以便继续进行

<img src="/img/your-first-task/your-first-task-7.png" alt="Reviewing a proposed file creation action" width="800" />
*Roo Code 会精确显示它想要执行的操作，并等待你的批准。*

**每个操作都需要你的明确批准**（除非启用了自动批准）：

*   **批准：** 点击“Approve”按钮执行建议的操作
*   **拒绝：** 点击“Reject”按钮，并根据需要提供反馈

---

## 第五步：迭代

Roo Code 以迭代的方式工作。在每个操作之后，它会等待你的反馈，然后再提出下一步建议。继续这个审查-批准的循环，直到你的任务完成。

<img src="/img/your-first-task/your-first-task-8.png" alt="Final result of a completed task showing the iteration process" width="500" />
*完成任务后，Roo Code 会显示最终结果并等待你的下一条指令。*

---

## 结论

你现在已经用 Roo Code 完成了你的第一个任务！通过这个过程，你已经学会了：

*   如何使用自然语言与 Roo Code 互动
*   基于批准的工作流程让你始终掌控一切
*   Roo Code 用来逐步解决问题的迭代方法

这种迭代的、基于批准的工作流程是 Roo Code 工作的核心——让 AI 处理繁琐的编码部分，而你则保持完全的监督。既然你已经了解了基础知识，你就可以开始处理更复杂的任务，探索不同的[模式](/basic-usage/using-modes)以适应专门的工作流程，或者尝试[自动批准功能](/features/auto-approving-actions)来加速重复性任务。
