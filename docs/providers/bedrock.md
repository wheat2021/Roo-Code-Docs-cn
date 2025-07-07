---
sidebar_label: AWS Bedrock
---

# 通过 Roo Code 使用 AWS Bedrock

Roo Code 支持通过 Amazon Bedrock 访问模型。Amazon Bedrock 是一项完全托管的服务，它通过单一 API 提供来自领先人工智能公司的一系列高性能基础模型 (FM)。

**网站：** [https://aws.amazon.com/bedrock/](https://aws.amazon.com/bedrock/)

---

## 先决条件

*   **AWS 账户：** 您需要一个有效的 AWS 账户。
*   **Bedrock 访问权限：** 您必须请求并获得 Amazon Bedrock 的访问权限。有关请求访问权限的详细信息，请参阅 [AWS Bedrock 文档](https://docs.aws.amazon.com/bedrock/latest/userguide/getting-started.html)。
*   **模型访问权限：** 在 Bedrock 中，您需要为您想使用的特定模型（例如 Anthropic Claude）请求访问权限。
*   **安装 AWS CLI：** 使用 AWS CLI 配置您的账户以进行身份验证。
    ```bash
     aws configure
    ```

---

## 获取凭证

您有两种主要方式来配置 AWS 凭证：

1.  **AWS 访问密钥（推荐用于开发）：**
    *   创建一个具有必要权限（至少 `bedrock:InvokeModel`）的 IAM 用户。
    *   为该用户生成一个访问密钥 ID 和秘密访问密钥。
    *   *（可选）* 如果您的 IAM 配置要求，请创建一个会话令牌。
2.  **AWS 配置文件：**
    *   使用 AWS CLI 或通过手动编辑您的 AWS 凭证文件来配置 AWS 配置文件。有关详细信息，请参阅 [AWS CLI 文档](https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-profiles.html)。

---

## 支持的模型

根据源代码，Roo Code 通过 Bedrock 支持以下模型：

*   **Amazon:**
    *   `amazon.nova-pro-v1:0`
    *   `amazon.nova-pro-latency-optimized-v1:0`
    *   `amazon.nova-lite-v1:0`
    *   `amazon.nova-micro-v1:0`
    *   `amazon.titan-text-lite-v1:0`
    *   `amazon.titan-text-express-v1:0`
    *   `amazon.titan-text-embeddings-v1:0`
    *   `amazon.titan-text-embeddings-v2:0`
*   **Anthropic:**
    *   `anthropic.claude-opus-4-20250514-v1:0`
    *   `anthropic.claude-sonnet-4-20250514-v1:0`
    *   `anthropic.claude-3-7-sonnet-20250219-v1:0`
    *   `anthropic.claude-3-5-sonnet-20241022-v2:0`
    *   `anthropic.claude-3-5-haiku-20241022-v1:0`
    *   `anthropic.claude-3-5-sonnet-20240620-v1:0`
    *   `anthropic.claude-3-opus-20240229-v1:0`
    *   `anthropic.claude-3-sonnet-20240229-v1:0`
    *   `anthropic.claude-3-haiku-20240307-v1:0`
    *   `anthropic.claude-2-1-v1:0`
    *   `anthropic.claude-2-0-v1:0`
    *   `anthropic.claude-instant-v1:0`
*   **DeepSeek:**
    *   `deepseek.r1-v1:0`
*   **Meta:**
    *   `meta.llama3-3-70b-instruct-v1:0`
    *   `meta.llama3-2-90b-instruct-v1:0`
    *   `meta.llama3-2-11b-instruct-v1:0`
    *   `meta.llama3-2-3b-instruct-v1:0`
    *   `meta.llama3-2-1b-instruct-v1:0`
    *   `meta.llama3-1-405b-instruct-v1:0`
    *   `meta.llama3-1-70b-instruct-v1:0`
    *   `meta.llama3-1-70b-instruct-latency-optimized-v1:0`
    *   `meta.llama3-1-8b-instruct-v1:0`
    *   `meta.llama3-70b-instruct-v1:0`
    *   `meta.llama3-8b-instruct-v1:0`

请参阅 [Amazon Bedrock 文档](https://docs.aws.amazon.com/bedrock/latest/userguide/models-supported.html)以获取最新的可用模型及其 ID 列表。在配置 Roo Code 时，请确保使用*模型 ID*，而不是模型名称。

---

## 在 Roo Code 中配置

1.  **打开 Roo Code 设置：** 在 Roo Code 面板中点击齿轮图标 (<Codicon name="gear" />)。
2.  **选择提供商：** 从“API 提供商”下拉菜单中选择“Bedrock”。
3.  **选择身份验证方法：**
    *   **AWS 凭证：**
        *   输入您的“AWS 访问密钥”和“AWS 秘密密钥”。
        *   （可选）如果您使用临时凭证，请输入您的“AWS 会话令牌”。
    *   **AWS 配置文件：**
        *   输入您的“AWS 配置文件”名称（例如，“default”）。
4.  **选择区域：** 选择您的 Bedrock 服务所在的 AWS 区域（例如，“us-east-1”）。
5.  **（可选）跨区域推理：** 如果您想访问与您配置的 AWS 区域不同的区域中的模型，请勾选“使用跨区域推理”。
6.  **（可选）VPC 端点：** 对于企业环境：
    *   勾选“使用 VPC 端点”以通过您的 VPC 端点路由所有 Bedrock API 调用。
    *   在出现的文本字段中输入您的 VPC 端点 URL。
    *   这可确保所有 LLM 事务都保留在您的公司网络内。
7.  **选择模型：** 从“模型”下拉菜单中选择您想要的模型。

---
---

## Claude 模型的推理预算

Roo Code 支持在 Bedrock 上为 Anthropic 的 Claude 模型使用推理预算（扩展思考）。这允许模型在响应之前进行更多“思考”，这对于复杂任务非常有用。

要启用推理预算：

1.  **选择一个支持的 Claude 模型**（例如，`anthropic.claude-3-sonnet-20240229-v1:0`）。
2.  在模型设置中**启用推理模式**。
3.  **调整思考预算**以控制模型应该“思考”多少。

此功能仅适用于支持的 Claude 模型。

## 提示和说明

*   **权限：** 确保您的 IAM 用户或角色具有调用 Bedrock 模型所需的权限。需要 `bedrock:InvokeModel` 权限。
*   **定价：** 有关模型成本的详细信息，请参阅 [Amazon Bedrock 定价](https://aws.amazon.com/bedrock/pricing/)页面。
*   **跨区域推理：** 使用跨区域推理可能会导致更高的延迟。
*   **VPC 端点：** 使用 VPC 端点时，请确保您的端点已正确配置以处理 Bedrock API 调用。此功能对于有严格安全要求、规定所有 API 流量必须保留在其私有网络内的组织特别有用。
