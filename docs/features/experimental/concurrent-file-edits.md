---
sidebar_label: '多文件编辑'
---

# 并发文件编辑（又称多文件编辑）

在单次操作中编辑多个文件，极大地加快了重构和多文件更改的速度。

---

## 功能介绍

<img src="/img/concurrent-file-edits/concurrent-file-edits-1.png" alt="显示多个文件更改的批量差异批准界面" width="800" />

并发文件编辑允许 Roo 在单个请求中修改工作区中的多个文件。您无需单独批准每个文件编辑，而是通过统一的批量批准界面一次性审查和批准所有更改。

---

## 为何使用

**传统方法**：需要单独批准的顺序文件编辑
- 编辑文件 A → 批准
- 编辑文件 B → 批准
- 编辑文件 C → 批准

**使用并发文件编辑**：所有更改一同呈现
- 审查文件 A、B 和 C 中的所有建议更改
- 一次性批准以应用所有更改

这减少了中断，并加快了复杂任务的速度，例如：
- 跨多个文件重构函数
- 在整个代码库中更新配置值
- 重命名组件及其引用
- 应用一致的格式或样式更改

---

## 如何启用

:::info 实验性功能
多文件编辑是一项实验性功能，必须在设置中启用。

1. 打开 Roo Code 设置（点击 Roo Code 中的齿轮图标）
2. 导航至 **Roo Code > 实验性设置**
3. 启用 **启用多文件编辑** 选项

<img src="/img/concurrent-file-edits/concurrent-file-edits.png" alt="在实验性设置中启用多文件编辑的切换开关" width="400" />
:::

---

## 使用此功能

启用后，Roo 会在适当时自动使用并发编辑。您将看到一个“批量差异批准”界面，显示：

- 所有待修改的文件
- 每个文件的建议更改
- 批准所有更改或单独审查的选项

### 示例工作流程

1. 要求 Roo “更新所有 API 端点以使用新的身份验证方法”
2. Roo 分析您的代码库并识别所有受影响的文件
3. 您会收到一个批量批准请求，其中显示了以下文件的更改：
   - `src/api/users.js`
   - `src/api/products.js`
   - `src/api/orders.js`
   - `src/middleware/auth.js`
4. 在统一的差异视图中审查所有更改
5. 批准以同时应用所有更改

---

## 技术细节

此功能利用了 [`apply_diff`](/advanced-usage/available-tools/apply-diff#experimental-multi-file-edits-multi_file_apply_diff) 工具的实验性多文件功能。有关实现、XML 格式以及 `MultiFileSearchReplaceDiffStrategy` 工作原理的详细信息，请参阅 [apply_diff 文档](/advanced-usage/available-tools/apply-diff#experimental-multi-file-edits-multi_file_apply_diff)。


---

## 最佳实践

### 何时启用
- 使用功能强大的人工智能模型（Claude 3.5 Sonnet、GPT-4 等）
- 习惯于一次性审查多个更改

### 何时禁用
- 使用可能难以处理复杂多文件上下文的较弱模型
- 倾向于单独审查每个更改

---

## 限制

- **实验性**：此功能仍在完善中，可能存在边缘情况
- **依赖模型**：在功能更强大的人工智能模型上效果最佳
- **令牌使用**：由于上下文较大，初始请求可能会使用更多令牌
- **复杂性**：非常大的批量操作可能更难审查

---

## 故障排除

### 更改未批量处理
- 验证实验性标志是否在设置中启用
- 检查您的模型是否支持多文件操作
- 确保文件未被 `.rooignore` 限制

### 批准界面未出现
- 更新到最新版本的 Roo Code
- 检查 VS Code 的输出面板中是否有错误
- 尝试禁用并重新启用该功能

### 性能问题
- 对于非常大的批量操作，请考虑将任务分解为更小的块
- 如果 API 配额有限，请监控令牌使用情况

---

## 另请参阅

- [`apply_diff` 工具文档](/advanced-usage/available-tools/apply-diff) - 详细技术信息
- [实验性功能](/features/experimental/experimental-features) - 其他实验性功能
- [`.rooignore` 配置](/features/rooignore) - 文件访问限制