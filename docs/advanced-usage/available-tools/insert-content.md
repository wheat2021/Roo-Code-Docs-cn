# insert_content

`insert_content` 工具可将新内容行添加到现有文件中，而无需修改原始内容。它非常适合在特定位置插入代码块、配置条目或日志行。

---

## 参数

该工具接受以下参数：

- `path` (必需): 要插入内容的文件相对于工作区根目录的路径。
- `line` (必需): 内容应插入到此行号（从 1 开始）*之前*。使用 `0` 可将内容附加到文件末尾。
- `content` (必需): 要插入的文本内容。

---

## 功能说明

此工具会读取目标文件，根据 `line` 参数确定指定的插入点，并将提供的 `content` 插入到该位置。如果 `line` 为 `0`，则内容将添加到末尾。更改会显示在差异视图中，供用户批准后保存。

---

## 使用场景

- 在文件开头添加新的导入语句时。
- 在现有代码中插入新函数或方法时。
- 在配置文件中添加配置块时。
- 附加日志条目或数据记录时。
- 在不更改现有行的情况下添加任何多行文本块时。

---

## 主要特性

- **精确定位插入**: 在指定的行号精确添加内容，或附加到文件末尾。
- **保留现有内容**: 不会修改或删除文件的原始行。
- **交互式批准**: 在差异视图中显示建议的插入内容，需要用户明确批准。
- **支持用户编辑**: 允许在最终批准前直接在差异视图中编辑建议的内容。
- **处理行号**: 正确解释 `line` 参数（从 1 开始，或 0 表示附加）。
- **上下文跟踪**: 记录文件编辑操作以进行上下文管理。
- **错误处理**: 检查缺失的参数、无效的行号和文件访问问题。

---

## 限制

- **仅限插入**: 无法替换或删除现有内容。如需修改，请使用 `apply_diff` 或 `search_and_replace`。
- **需要现有文件**: `path` 指定的目标文件必须存在。
- **审查开销**: 强制性的差异视图批准增加了一个交互步骤。

---

## 工作原理

当调用 `insert_content` 工具时，它会遵循以下流程：

1.  **参数验证**: 检查必需的 `path`、`line` 和 `content`。验证 `line` 是否为非负整数。
2.  **文件读取**: 读取 `path` 指定的目标文件的内容。
3.  **计算插入点**: 将基于 1 的 `line` 参数转换为基于 0 的索引以进行内部处理（`-1` 用于附加）。
4.  **内容插入**: 使用内部实用程序 (`insertGroups`) 将原始文件行与新的 `content` 在计算出的索引位置合并。
5.  **差异视图交互**:
    *   在差异视图中打开文件 (`cline.diffViewProvider.open`)。
    *   使用建议的内容更新差异视图 (`cline.diffViewProvider.update`)。
6.  **用户批准**: 通过 `askApproval` 提交更改。如果被拒绝则还原。
7.  **保存更改**: 如果获得批准，则使用 `cline.diffViewProvider.saveChanges` 保存更改。
8.  **文件上下文跟踪**: 使用 `cline.getFileContextTracker().trackFileContext` 跟踪编辑。
9.  **处理用户编辑**: 如果用户在差异视图中编辑了内容，则报告最终合并的内容。
10. **结果报告**: 向 AI 模型报告成功（包括用户编辑）或失败。

---

## 使用示例

在文件开头插入导入语句 (`line: 1`):

```xml
<insert_content>
<path>src/utils.ts</path>
<line>1</line>
<content>
// 在文件开头添加导入
import { sum } from './math';
import { parse } from 'date-fns';
</content>
</insert_content>
```

将内容附加到文件末尾 (`line: 0`):

```xml
<insert_content>
<path>config/routes.yaml</path>
<line>0</line>
<content>
- path: /new-feature
  component: NewFeatureComponent
  auth_required: true
</content>
</insert_content>
```

在第 50 行之前插入一个函数:

```xml
<insert_content>
<path>src/services/api.js</path>
<line>50</line>
<content>
async function fetchUserData(userId) {
  const response = await fetch(`/api/users/${userId}`);
  if (!response.ok) {
    throw new Error('Failed to fetch user data');
  }
  return response.json();
}
</content>
</insert_content>