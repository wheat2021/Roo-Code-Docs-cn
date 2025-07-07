---
sidebar_label: LiteLLM
---

# 将 LiteLLM 与 Roo Code 结合使用

LiteLLM 是一个功能强大的工具，它通过提供与 OpenAI 兼容的 API，为超过 100 种大型语言模型（LLM）提供了统一的接口。这使您能够运行一个本地服务器，该服务器可以将请求代理到各种模型提供商或提供本地模型，所有这些都可以通过一个一致的 API 端点进行访问。

**网站：** [https://litellm.ai/](https://litellm.ai/) (主项目) & [https://docs.litellm.ai/](https://docs.litellm.ai/) (文档)

---

## 主要优势

*   **统一 API：** 通过单个与 OpenAI 兼容的 API 访问各种 LLM（来自 OpenAI、Anthropic、Cohere、HuggingFace 等）。
*   **本地部署：** 在本地运行您自己的 LiteLLM 服务器，从而更好地控制模型访问并可能减少延迟。
*   **简化配置：** 在一个地方（您的 LiteLLM 服务器）管理凭据和模型配置，并让 Roo Code 连接到它。
*   **成本管理：** LiteLLM 提供跨不同模型和提供商跟踪成本的功能。

---

## 设置您的 LiteLLM 服务器

要将 LiteLLM 与 Roo Code 结合使用，您首先需要设置并运行一个 LiteLLM 服务器。

1.  **安装：** 遵循官方的 [LiteLLM 安装指南](https://docs.litellm.ai/docs/proxy_server) 来安装 LiteLLM 及其依赖项。
2.  **配置：** 使用您想要使用的模型配置您的 LiteLLM 服务器。这通常涉及在 LiteLLM 服务器的配置中为底层提供商（例如 OpenAI、Anthropic）设置 API 密钥。
3.  **启动服务器：** 运行您的 LiteLLM 服务器。默认情况下，它通常在 `http://localhost:4000` 上启动。
    *   您还可以为您的 LiteLLM 服务器本身配置一个 API 密钥以增加安全性。

有关服务器设置、模型配置和高级功能的详细说明，请参阅 [LiteLLM 文档](https://docs.litellm.ai/docs/)。

---

## 在 Roo Code 中配置

一旦您的 LiteLLM 服务器正在运行：

1.  **打开 Roo Code 设置：** 单击 Roo Code 面板中的齿轮图标 (<Codicon name="gear" />)。
2.  **选择提供商：** 从“API 提供商”下拉菜单中选择“LiteLLM”。
3.  **输入基础 URL：**
    *   输入您的 LiteLLM 服务器的 URL。
    *   如果留空，则默认为 `http://localhost:4000`。
4.  **输入 API 密钥（可选）：**
    *   如果您为 LiteLLM 服务器配置了 API 密钥，请在此处输入。
    *   如果您的 LiteLLM 服务器不需要 API 密钥，Roo Code 将使用一个默认的虚拟密钥（`"dummy-key"`），这应该可以正常工作。
5.  **选择模型：**
    *   Roo Code 将尝试通过查询 `${baseUrl}/v1/model/info` 端点从您的 LiteLLM 服务器获取可用模型列表。
    *   下拉菜单中显示的模型来源于此端点。
    *   如果您向 LiteLLM 服务器添加了新模型，请使用刷新按钮更新模型列表。
    *   如果未选择任何模型，Roo Code 将默认为 `anthropic/claude-3-7-sonnet-20250219`（这是 `litellmDefaultModelId`）。请确保此模型（或您期望的默认模型）已在您的 LiteLLM 服务器上配置并可用。

<img src="/img/litellm/litellm.png" alt="Roo Code LiteLLM 提供商设置" width="600" />

---

## Roo Code 如何获取和解释模型信息

当您配置 LiteLLM 提供商时，Roo Code 会与您的 LiteLLM 服务器交互以获取有关可用模型的详细信息：

*   **模型发现：** Roo Code 向您的 LiteLLM 服务器上的 `${baseUrl}/v1/model/info` 发出 GET 请求。如果在 Roo Code 的设置中提供了 API 密钥，它将包含在 `Authorization: Bearer ${apiKey}` 头中。
*   **模型属性：** 对于您的 LiteLLM 服务器报告的每个模型，Roo Code 会提取并解释以下内容：
    *   `model_name`：模型的标识符。
    *   `maxTokens`：最大输出令牌数。如果 LiteLLM 未指定，则默认为 `8192`。
    *   `contextWindow`：最大上下文令牌数。如果 LiteLLM 未指定，则默认为 `200000`。
    *   `supportsImages`：由 LiteLLM 提供的 `model_info.supports_vision` 确定。
    *   `supportsPromptCache`：由 LiteLLM 提供的 `model_info.supports_prompt_caching` 确定。
    *   `inputPrice` / `outputPrice`：根据 LiteLLM 的 `model_info.input_cost_per_token` 和 `model_info.output_cost_per_token` 计算。
    *   `supportsComputerUse`：如果底层模型标识符（来自 `litellm_params.model`，例如 `openrouter/anthropic/claude-3.5-sonnet`）与 Roo Code 中预定义为适合“计算机使用”的某个 Anthropic 模型匹配，则此标志设置为 `true`（请参阅技术细节中的 `COMPUTER_USE_MODELS`）。

如果您的 LiteLLM 服务器的 `/model/info` 端点未为给定模型明确提供这些属性，Roo Code 会使用默认值。默认值为：
*   `maxTokens`：8192
*   `contextWindow`：200,000
*   `supportsImages`：`true`
*   `supportsComputerUse`：`true`（对于默认模型 ID）
*   `supportsPromptCache`：`true`
*   `inputPrice`：3.0（每 1k 令牌的微美分）
*   `outputPrice`：15.0（每 1k 令牌的微美分）

---

## 提示和说明

*   **LiteLLM 服务器是关键：** 模型、下游提供商（如 OpenAI、Anthropic）的 API 密钥以及其他高级功能的主要配置都在您的 LiteLLM 服务器上管理。Roo Code 充当此服务器的客户端。
*   **模型可用性：** Roo Code 的“模型”下拉菜单中可用的模型完全取决于您的 LiteLLM 服务器通过其 `/v1/model/info` 端点公开的内容。
*   **网络可访问性：** 确保您的 LiteLLM 服务器正在运行，并且可以从运行 VS Code 和 Roo Code 的计算机上访问（例如，如果不在 `localhost` 上，请检查防火墙规则）。
*   **故障排除：** 如果模型未出现或请求失败：
    *   验证您的 LiteLLM 服务器是否正在运行并已正确配置。
    *   检查 LiteLLM 服务器日志以查找错误。
    *   确保 Roo Code 设置中的基础 URL 与您的 LiteLLM 服务器地址匹配。
    *   确认您的 LiteLLM 服务器所需的任何 API 密钥已在 Roo Code 中正确输入。
*   **计算机使用模型：** Roo Code 中的 `supportsComputerUse` 标志主要与某些已知在工具使用和函数调用任务方面表现良好的 Anthropic 模型相关。如果您通过 LiteLLM 路由其他模型，则此标志可能不会自动设置，除非底层模型 ID 与 Roo Code 识别的特定 Anthropic 模型匹配。

通过利用 LiteLLM，您可以显著扩展 Roo Code 可访问的模型范围，同时集中管理它们。