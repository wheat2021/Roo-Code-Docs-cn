# access_mcp_resource

`access_mcp_resource` 工具从已连接的“模型上下文协议”（MCP）服务器暴露的资源中检索数据。它允许 Roo 访问文件、API 响应、文档或系统信息，为任务提供额外的上下文。

---

## 参数

该工具接受以下参数：

- `server_name` (必需): 提供资源的 MCP 服务器的名称。
- `uri` (必需): 标识要访问的特定资源的 URI。

---

## 功能

此工具连接到 MCP 服务器并从其暴露的资源中获取数据。与执行操作的 `use_mcp_tool` 不同，此工具专门检索用作任务上下文的信息。

---

## 使用时机

- 当 Roo 需要来自外部系统的额外上下文时。
- 当 Roo 需要从专门的 MCP 服务器访问特定领域的数据时。
- 当 Roo 需要检索由 MCP 服务器托管的参考文档时。
- 当 Roo 需要通过 MCP 集成来自外部 API 的实时数据时。

---

## 主要特性

- 从 MCP 资源中检索文本和图像数据。
- 在执行资源访问前需要用户批准。
- 使用基于 URI 的寻址方式精确识别资源。
- 与“模型上下文协议”SDK 集成。
- 根据内容类型适当显示资源内容。
- 支持超时以实现可靠的网络操作。
- 处理服务器连接状态（已连接、连接中、已断开）。
- 从已连接的服务器发现可用资源。
- 处理带有元数据的结构化响应数据。
- 处理图像内容的特殊渲染。

---

## 限制

- 依赖于外部 MCP 服务器的可用性和连接状态。
- 仅限于已连接服务器提供的资源。
- 无法访问已禁用服务器的资源。
- 网络问题可能会影响可靠性和性能。
- 资源访问受配置的超时限制。
- URI 格式由具体的 MCP 服务器实现决定。
- 不具备离线或缓存资源访问能力。

---

## 工作原理

当调用 `access_mcp_resource` 工具时，它会遵循以下流程：

1.  **连接验证**:
    -   验证 MCP 中心是否可用并已初始化。
    -   确认指定的服务器存在于连接列表中。
    -   检查服务器是否被禁用（如果是，则返回错误）。

2.  **用户批准**:
    -   向用户呈现资源访问请求以供批准。
    -   提供服务器名称和资源 URI 供用户验证。
    -   仅在用户批准资源访问后继续。

3.  **资源请求**:
    -   使用“模型上下文协议”SDK 与服务器通信。
    -   通过 MCP 中心向服务器发出 `resources/read` 请求。
    -   应用配置的超时以防止在无响应的服务器上挂起。

4.  **响应处理**:
    -   接收带有元数据和内容数组的结构化响应。
    -   处理文本内容以显示给用户。
    -   特殊处理图像数据以便适当显示。
    -   将处理后的资源数据返回给 Roo，用于当前任务。

---

## 资源类型

MCP 服务器可以提供两种主要类型的资源：

1.  **标准资源**:
    -   具有特定 URI 的固定资源。
    -   定义了名称、描述和 MIME 类型。
    -   无需参数即可直接访问。
    -   通常代表静态数据或实时信息。

2.  **资源模板**:
    -   URI 中带有占位符值的参数化资源。
    -   允许根据提供的参数动态生成资源。
    -   可以代表查询或数据的筛选视图。
    -   更灵活但需要额外的 URI 格式化。

---

## 使用案例

- 在协助 API 开发时，Roo 从 MCP 资源中检索端点规范以确保正确实现。
- 在协助数据可视化时，Roo 从连接的 MCP 服务器访问当前数据样本。
- 在特定领域工作时，Roo 检索技术文档以提供准确的指导。
- 在生成行业特定代码时，Roo 从文档资源中引用合规性要求。

---

## 用法示例

访问当前天气数据：
```
<access_mcp_resource>
<server_name>weather-server</server_name>
<uri>weather://san-francisco/current</uri>
</access_mcp_resource>
```

检索 API 文档：
```
<access_mcp_resource>
<server_name>api-docs</server_name>
<uri>docs://payment-service/endpoints</uri>
</access_mcp_resource>
```

访问特定领域的知识：
```
<access_mcp_resource>
<server_name>knowledge-base</server_name>
<uri>kb://medical/terminology/common</uri>
</access_mcp_resource>
```

获取系统配置：
```
<access_mcp_resource>
<server_name>infra-monitor</server_name>
<uri>config://production/database</uri>
</access_mcp_resource>
