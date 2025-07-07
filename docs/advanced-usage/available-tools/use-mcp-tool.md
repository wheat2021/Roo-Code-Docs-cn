# use_mcp_tool

`use_mcp_tool` 工具能够与已连接的“模型上下文协议”（MCP）服务器提供的外部工具进行交互。它通过一个标准化协议，用特定领域的功能扩展了 Roo 的能力。

---

## 参数

该工具接受以下参数：

- `server_name` (必需): 提供该工具的 MCP 服务器名称。
- `tool_name` (必需): 要执行的工具名称。
- `arguments` (必需/可选): 一个 JSON 对象，包含工具的输入参数，遵循工具的输入模式。对于不需要输入的工具，此参数可能为可选。

---

## 功能说明

该工具允许 Roo 访问由外部 MCP 服务器提供的专业功能。每个 MCP 服务器可以提供多个具有独特功能的工具，从而扩展 Roo 的内置功能。系统会根据模式验证参数，管理服务器连接，并处理各种内容类型的响应（文本、图像、资源）。

---

## 使用场景

- 当需要核心工具中没有的专业功能时
- 当需要执行特定领域的操作时
- 当需要与外部系统或服务集成时
- 当处理需要特定处理或分析的数据时
- 当通过标准化接口访问专有工具时

---

## 主要特性

- 使用标准化的 MCP 协议，通过 `@modelcontextprotocol/sdk` 库实现
- 支持多种传输机制（StdioClientTransport、StreamableHTTPClientTransport 和 SSEClientTransport）
- 在客户端和服务器端使用 Zod 模式验证参数
- 处理多种响应内容类型：文本、图像和资源引用
- 当服务器代码更改时，通过自动重启管理服务器生命周期
- 提供“始终允许”机制，以绕过对受信任工具的审批
- 与配套的 `access_mcp_resource` 工具协同工作，用于资源检索
- 对失败的操作进行适当的错误跟踪和处理
- 支持可配置的超时（1-3600 秒，默认为 60 秒）
- 允许文件监视器自动检测并重新加载服务器更改

---

## 限制

- 依赖于外部 MCP 服务器的可用性和连接状态
- 仅限于已连接服务器提供的工具
- 不同 MCP 服务器的工具能力各不相同
- 网络问题可能会影响可靠性和性能
- 执行前需要用户批准（除非在“始终允许”列表中）
- 无法同时执行多个 MCP 工具操作

---

## 服务器配置

MCP 服务器可以在全局或项目级别进行配置：

- **全局配置**: 通过 VS Code 中的 Roo Code 扩展设置进行管理。除非被覆盖，否则这些设置适用于所有项目。
- **项目级配置**: 在项目根目录下的 `.roo/mcp.json` 文件中定义。
  - 这允许项目特定的服务器设置。
  - 如果项目级服务器与全局服务器同名，则项目级服务器优先。
  - 由于 `.roo/mcp.json` 可以提交到版本控制系统，因此简化了与团队共享配置的过程。

---

## 工作原理

当调用 `use_mcp_tool` 工具时，它会遵循以下流程：

1.  **初始化与验证**:
    - 系统验证 MCP 中心是否可用。
    - 确认指定的服务器存在且已连接。
    - 验证请求的工具在服务器上是否存在。
    - 根据工具的模式定义验证参数。
    - 从服务器配置中提取超时设置（默认为 60 秒）。

2.  **执行与通信**:
    - 系统选择适当的传输机制：
      - `StdioClientTransport`: 用于通过标准 I/O 与本地进程通信。
      - `SSEClientTransport`: 用于通过服务器发送事件（Server-Sent Events）与 HTTP 服务器通信。
      - `StreamableHTTPClientTransport`: 用于通过可流式 HTTP 事件与 HTTP 服务器通信。
    - 发送一个包含经过验证的服务器名称、工具名称和参数的请求。
    - 通信使用 `@modelcontextprotocol/sdk` 库进行标准化交互。
    - 请求执行过程会被跟踪，并带有超时处理，以防止操作挂起。

3.  **响应处理**:
    - 响应可以包含多种内容类型：
      - 文本内容：纯文本响应。
      - 图像内容：带有 MIME 类型信息的二进制图像数据。
      - 资源引用：用于访问服务器资源的 URI（与 `access_mcp_resource` 协同工作）。
    - 系统检查 `isError` 标志以确定是否需要错误处理。
    - 结果被格式化以便在 Roo 界面中显示。

4.  **资源与错误处理**:
    - 系统使用 WeakRef 模式以防止内存泄漏。
    - 一个连续错误计数器用于跟踪和管理错误。
    - 文件监视器监控服务器代码的更改并触发自动重启。
    - 安全模型要求执行工具前需获得批准，除非在“始终允许”列表中。

---

## 安全与权限

MCP 架构提供了几个安全特性：

- 用户在执行工具前必须批准（默认情况下）。
- 特定工具可以在“始终允许”列表中标记为自动批准。
- 服务器配置使用 Zod 模式进行验证以确保完整性。
- 可配置的超时防止操作挂起（1-3600 秒）。
- 可以通过用户界面启用或禁用服务器连接。

---

## 使用示例场景

- 使用服务器端处理工具分析专门的数据格式。
- 通过托管在外部服务器上的人工智能模型生成图像或其他媒体。
- 无需本地实现即可执行复杂的特定领域计算。
- 通过受控接口访问专有 API 或服务。
- 从专门的数据库或数据源检索数据。

---

## 用法示例

请求天气预报数据并获得文本响应：
```
<use_mcp_tool>
<server_name>weather-server</server_name>
<tool_name>get_forecast</tool_name>
<arguments>
{
  "city": "San Francisco",
  "days": 5,
  "format": "text"
}
</arguments>
</use_mcp_tool>
```

使用专门的工具分析源代码，该工具返回 JSON：
```
<use_mcp_tool>
<server_name>code-analysis</server_name>
<tool_name>complexity_metrics</tool_name>
<arguments>
{
  "language": "typescript",
  "file_path": "src/app.ts",
  "include_functions": true,
  "metrics": ["cyclomatic", "cognitive"]
}
</arguments>
</use_mcp_tool>
```

使用特定参数生成图像：
```
<use_mcp_tool>
<server_name>image-generation</server_name>
<tool_name>create_image</tool_name>
<arguments>
{
  "prompt": "A futuristic city with flying cars",
  "style": "photorealistic",
  "dimensions": {
    "width": 1024,
    "height": 768
  },
  "format": "webp"
}
</arguments>
</use_mcp_tool>
```

通过返回资源引用的工具访问资源：
```
<use_mcp_tool>
<server_name>database-connector</server_name>
<tool_name>query_and_store</tool_name>
<arguments>
{
  "database": "users",
  "type": "select",
  "fields": ["name", "email", "last_login"],
  "where": {
    "status": "active"
  },
  "store_as": "active_users"
}
</arguments>
</use_mcp_tool>
```

不带必需参数的工具：
```
<use_mcp_tool>
<server_name>system-monitor</server_name>
<tool_name>get_current_status</tool_name>
<arguments>
{}
</arguments>
</use_mcp_tool>
