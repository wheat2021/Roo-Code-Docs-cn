---
title: 推荐的 MCP 服务器
sidebar_label: 推荐的 MCP 服务器
---

# 推荐的 MCP 服务器

尽管 Roo Code 可以连接任何遵循模型上下文协议（MCP）规范的服务器，但社区已经构建了几个开箱即用的高质量服务器。本页精选了我们**积极推荐**的服务器，并提供分步设置说明，让您在几分钟内就能开始高效工作。

> 我们会持续更新此列表。如果您维护的服务器希望我们考虑收录，请提交一个 pull-request。

---

## Context7

`Context7` 是我们的首选通用 MCP 服务器。它提供了一系列备受欢迎的工具，只需一条命令即可安装，并在所有支持 MCP 的主流编辑器中提供出色的支持。

### 我们推荐 Context7 的原因

*   **一键安装** – 所有内容都已打包，无需本地构建步骤。
*   **跨平台** – 可在 macOS、Windows、Linux 或 Docker 内部运行。
*   **积极维护** – Upstash 团队频繁更新。
*   **丰富的工具集** – 数据库访问、网页搜索、文本工具等。
*   **开源** – 在 MIT 许可下发布。

---

## 在 Roo Code 中安装 Context7

注册该服务器有两种常用方法：

1.  **全局配置** – 在每个工作区中都可用。
2.  **项目级配置** – 与您的代码一起检入版本控制。

下面我们将分别介绍这两种方法。

### 1. 全局配置

1.  点击 <Codicon name="server" /> 图标，打开 Roo Code 的 **MCP 设置**面板。
2.  点击 **编辑全局 MCP**。
3.  将下面的 JSON 粘贴到 `mcpServers` 对象内并保存。

```json
{
  "mcpServers": {
    "context7": {
      "command": "npx",
      "args": ["-y", "@upstash/context7-mcp@latest"]
    }
  }
}
```

**Windows (cmd.exe) 版本**

```json
{
  "mcpServers": {
    "context7": {
      "type": "stdio",
      "command": "cmd",
      "args": ["/c", "npx", "-y", "@upstash/context7-mcp@latest"]
    }
  }
}
```

同样在 **Windows (cmd)** 上，您可能需要通过 `cmd.exe` 来调用 `npx`：

<img src="/img/recommended-mcp-servers/context7-global-setup-fixed.png" alt="将 Context7 添加到全局 MCP 设置中" width="600" />

### 2. 项目级配置

如果您希望将配置提交到您的仓库，请在项目根目录下创建一个名为 `.roo/mcp.json` 的文件，并添加相同的代码片段：

```json
{
  "mcpServers": {
    "context7": {
      "command": "npx",
      "args": ["-y", "@upstash/context7-mcp@latest"]
    }
  }
}
```

**Windows (cmd.exe) 版本**

```json
{
  "mcpServers": {
    "context7": {
      "type": "stdio",
      "command": "cmd",
      "args": ["/c", "npx", "-y", "@upstash/context7-mcp@latest"]
    }
  }
}
```

<img src="/img/recommended-mcp-servers/context7-project-setup-fixed.png" alt="将 Context7 添加到项目级 MCP 文件中" width="600" />

> 当全局和项目文件定义了同名服务器时，**项目配置优先**。

---

## 验证安装

1.  确保在 MCP 设置面板中已开启 **启用 MCP 服务器**。
2.  您现在应该能看到 **Context7**。如果它尚未运行，请点击 <Codicon name="activate" /> 开关以启动它。
3.  当首次调用 Context7 工具时，Roo Code 会提示您。批准请求以继续。

<img src="/img/recommended-mcp-servers/context7-running-fixed.png" alt="Context7 在 Roo Code 中运行" width="400" />

---

## 后续步骤

*   在服务器窗格中浏览 Context7 附带的工具列表。
*   为您最常使用的工具配置 **始终允许**，以简化您的工作流程。
*   想要暴露您自己的 API？请查看 [MCP 服务器创建指南](/features/mcp/using-mcp-in-roo#enabling-or-disabling-mcp-server-creation)。

在寻找其他服务器？请关注本页——我们很快会添加更多推荐！