---
sidebar_label: GCP Vertex AI
---

# 通过 Roo Code 使用 GCP Vertex AI

Roo Code 支持通过谷歌云平台（Google Cloud Platform）的 Vertex AI 访问模型。Vertex AI 是一个托管的机器学习平台，提供对多种基础模型的访问，包括 Anthropic 的 Claude 系列模型。

**网站：** [https://cloud.google.com/vertex-ai](https://cloud.google.com/vertex-ai)

---

## 先决条件

*   **谷歌云账户：** 您需要一个有效的谷歌云平台（GCP）账户。
*   **项目：** 您需要一个已启用 Vertex AI API 的 GCP 项目。
*   **模型访问权限：** 您必须申请并获得想要在 Vertex AI 上使用的特定 Claude 模型的访问权限。具体说明请参阅 [谷歌云文档](https://cloud.google.com/vertex-ai/generative-ai/docs/partner-models/use-claude#before_you_begin)。
*   **应用默认凭证（ADC）：** Roo Code 使用应用默认凭证向 Vertex AI 进行身份验证。设置此项最简单的方法是：
    1.  安装 Google Cloud CLI：[https://cloud.google.com/sdk/docs/install](https://cloud.google.com/sdk/docs/install)
    2.  使用以下命令进行身份验证：`gcloud auth application-default login`
*   **服务账户密钥（备选方案）：** 或者，您也可以使用谷歌云服务账户密钥文件进行身份验证。您需要在您的 GCP 项目中生成此密钥。请参阅[关于创建服务账户密钥的谷歌云文档](https://cloud.google.com/iam/docs/creating-managing-service-account-keys)。

---

## 支持的模型

Roo Code 通过 Vertex AI 支持以下模型（基于源代码）：

*   **Google Gemini 模型：**
    *   `gemini-2.5-flash-preview-05-20`
    *   `gemini-2.0-flash-001`
    *   `gemini-2.5-pro-exp-03-25`
    *   `gemini-2.0-pro-exp-02-05`
    *   `gemini-2.0-flash-lite-001`
    *   `gemini-2.0-flash-thinking-exp-01-21`
    *   `gemini-1.5-flash-002`
    *   `gemini-1.5-pro-002`
*   **Anthropic Claude 模型：**
    *   `claude-opus-4@20250514:thinking`
    *   `claude-opus-4@20250514`
    *   `claude-sonnet-4@20250514:thinking`
    *   `claude-sonnet-4@20250514`
    *   `claude-3-7-sonnet@20250219:thinking`
    *   `claude-3-7-sonnet@20250219`
    *   `claude-3-5-sonnet-v2@20241022`
    *   `claude-3-5-sonnet@20240620`
    *   `claude-3-5-haiku@20241022`
    *   `claude-3-opus@20240229`
    *   `claude-3-haiku@20240307`

有关可用模型及其 ID 的最新列表，请参阅[谷歌云关于 Vertex AI 模型的文档](https://cloud.google.com/vertex-ai/generative-ai/docs/learn/models)。

---

## 在 Roo Code 中配置

1.  **打开 Roo Code 设置：** 点击 Roo Code 面板中的齿轮图标 (<Codicon name="gear" />)。
2.  **选择提供商：** 从“API 提供商”下拉菜单中选择“GCP Vertex AI”。
3.  **配置身份验证：**
    *   **如果使用应用默认凭证（ADC）：** 此处无需进一步操作。如果 ADC 配置正确（见先决条件），它将被自动使用。
    *   **如果不使用 ADC（服务账户密钥）：**
        *   **选项 A：粘贴 JSON 内容：** 将您的服务账户 JSON 密钥文件的全部内容粘贴到 **Google Cloud Credentials** 字段中。
        *   **选项 B：提供文件路径：** 在 **Google Cloud Key File Path** 字段中输入您下载的服务账户 JSON 密钥文件的绝对路径。
4.  **输入项目 ID：** 输入您的谷歌云项目 ID。
5.  **选择区域：** 选择您的 Vertex AI 资源所在的区域（例如，`us-east5`）。
6.  **选择模型：** 从“模型”下拉菜单中选择您想要的模型。
---

## 提示与说明

*   **权限：** 确保您的谷歌云账户拥有访问 Vertex AI 和您想使用的特定模型所需的权限。
*   **定价：** 详情请参阅 [Vertex AI 定价](https://cloud.google.com/vertex-ai/pricing) 页面。
