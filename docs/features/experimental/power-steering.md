---
sidebar_label: '动力转向'
---
import Codicon from '@site/src/components/Codicon';

# 动力转向（实验性功能）

“动力转向”实验性功能（`POWER_STEERING`）旨在通过更频繁地提醒底层大型语言模型（LLM）其当前模式定义和任何自定义指令，来增强 Roo Code 响应的一致性。

---

## 工作原理

启用动力转向后，Roo Code 会不断强化 LLM 对其指定角色（例如，“你是一个乐于助人的编程助手”）和用户提供的任何特定指南（例如，“始终使用 Python 提供代码示例”）的理解。

这是通过在每次交互中发送给 LLM 的信息中明确包含 `modeDetails.roleDefinition` 和 `modeDetails.customInstructions` 来实现的。

**目标：**
主要目标是确保 LLM 更严格地遵守其定义的角色，并更一致地遵循用户特定的指令。如果您发现 Roo 偏离其角色或忽略自定义规则，动力转向可以帮助其保持专注。

**权衡：**
这些频繁的提醒会在发送给 LLM 的每条消息中消耗额外的令牌。这意味着：
*   每条消息的令牌使用量增加。
*   可能导致更高的运营成本。
*   上下文窗口可能会更快被填满。

这是在更严格地遵守指令和资源消耗之间取得的平衡。

**默认状态：** 已禁用。

---

## 技术细节

*   **实验 ID：** `powerSteering`
*   **机制：**
    *   该功能的状态由 `getEnvironmentDetails` 函数检查。
    *   如果启用，当前模式的 `roleDefinition` 和 `customInstructions` 将被添加到发送给 LLM 的详细信息中。
    *   这些详细信息被包裹在 `<environment_details>` 标签中，并成为每次 LLM 交互上下文的一部分。
*   **影响：** 通过频繁包含角色定义和自定义指令，引导 LLM 生成更符合这些参数的响应。

---

## 启用此功能

动力转向在 Roo Code 高级设置的“实验性功能”部分进行管理。

1.  打开 Roo Code 设置（右上角的 <Codicon name="gear" /> 图标）。
2.  导航到“高级设置”。
3.  找到“实验性功能”区域。
4.  切换“动力转向”选项。
5.  保存您的更改。
<img src="/img/power-steering/power-steering.png" alt="智能上下文压缩和动力转向的设置" width="600" />

有关实验性功能的一般信息，请参阅[实验性功能概述](/features/experimental/experimental-features)。

---

## 反馈

请在 [Roo Code GitHub Issues 页面](https://github.com/RooCodeInc/Roo-Code/issues)上报告有关此功能的任何问题或建议。您的反馈对于改进 Roo Code 至关重要。