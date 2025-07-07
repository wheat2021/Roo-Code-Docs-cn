---
sidebar_label: 连接到 AI 提供商
---
import KangarooIcon from '@site/src/components/KangarooIcon';

# 连接你的第一个 AI 提供商

Roo Code 需要一个来自 AI 模型提供商的 API 密钥才能运行。我们推荐以下选项来访问强大的 **Claude 3.7 Sonnet** 模型：

- **OpenRouter (推荐):** 通过单个 API 密钥提供对多个 AI 模型的访问。非常适合以最少的设置快速入门。 [查看定价](https://openrouter.ai/models?order=pricing-low-to-high)。
- **Anthropic:** 直接访问 Claude 模型。需要 API 访问批准，并且可能会根据您的等级有[速率限制](https://docs.anthropic.com/en/api/rate-limits#requirements-to-advance-tier)。有关详细信息，请参阅 [Anthropic 的定价页面](https://www.anthropic.com/pricing#anthropic-api)。

---

## 获取你的 API 密钥

### 选项 1: LLM 路由器

LLM 路由器让你可以用一个 API 密钥访问多个 AI 模型，从而简化成本管理和模型切换。与直接提供商相比，它们通常提供[有竞争力的定价](https://openrouter.ai/models?order=pricing-low-to-high)。

#### OpenRouter

1. 前往 [openrouter.ai](https://openrouter.ai/)
2. 使用你的 Google 或 GitHub 帐户登录
3. 导航到 [API 密钥页面](https://openrouter.ai/keys) 并创建一个新密钥
4. 复制你的 API 密钥 - 你将在 Roo Code 设置中需要它

<img src="/img/connecting-api-provider/connecting-api-provider-4.png" alt="OpenRouter API 密钥页面" width="600" />

*OpenRouter 仪表板，带有“创建密钥”按钮。命名你的密钥并在创建后复制它。*

#### Requesty

1. 前往 [requesty.ai](https://requesty.ai/)
2. 使用你的 Google 帐户或电子邮件登录
3. 导航到 [API 管理页面](https://app.requesty.ai/api-keys) 并创建一个新密钥
4. **重要提示：** 请立即复制你的 API 密钥，因为它不会再次显示

<img src="/img/connecting-api-provider/connecting-api-provider-7.png" alt="Requesty API 管理页面" width="600" />

*Requesty API 管理页面，带有“创建 API 密钥”按钮。立即复制你的密钥 - 它只显示一次。*

### 选项 2: 直接提供商

为了直接从其原始提供商处访问特定模型，并完全访问其功能和能力：

#### Anthropic

1. 前往 [console.anthropic.com](https://console.anthropic.com/)
2. 注册一个帐户或登录
3. 导航到 [API 密钥部分](https://console.anthropic.com/settings/keys) 并创建一个新密钥
4. **重要提示：** 请立即复制你的 API 密钥，因为它不会再次显示

<img src="/img/connecting-api-provider/connecting-api-provider-5.png" alt="Anthropic 控制台 API 密钥部分" width="600" />

*Anthropic 控制台 API 密钥部分，带有“创建密钥”按钮。命名你的密钥，设置到期日，并立即复制它。*

#### OpenAI

1. 前往 [platform.openai.com](https://platform.openai.com/)
2. 注册一个帐户或登录
3. 导航到 [API 密钥部分](https://platform.openai.com/api-keys) 并创建一个新密钥
4. **重要提示：** 请立即复制你的 API 密钥，因为它不会再次显示

<img src="/img/connecting-api-provider/connecting-api-provider-6.png" alt="OpenAI API 密钥页面" width="600" />

*OpenAI 平台，带有“创建新的秘密密钥”按钮。命名你的密钥并在创建后立即复制它。*

---

## 在 VS Code 中配置 Roo Code

一旦你有了 API 密钥：

1. 在 VS Code 的活动栏中点击 Roo Code 图标 (<KangarooIcon />) 来打开 Roo Code 侧边栏
2. 在欢迎屏幕中，从下拉菜单中选择你的 API 提供商
3. 将你的 API 密钥粘贴到相应的字段中
4. 选择你的模型：
   - 对于 **OpenRouter**：选择 `anthropic/claude-3.7-sonnet` ([模型详情](https://openrouter.ai/anthropic/claude-3.7-sonnet))
   - 对于 **Anthropic**：选择 `claude-3-7-sonnet-20250219` ([模型详情](https://www.anthropic.com/pricing#anthropic-api))

:::info 模型选择建议
我们强烈推荐 **Claude 3.7 Sonnet** 以获得最佳体验——它通常开箱即用。Roo Code 已针对该模型的能力和指令遵循行为进行了广泛优化。

选择替代模型是一项引入复杂性的高级功能。不同模型在遵循工具指令、解析格式以及在多步操作中维护上下文方面差异很大。如果你确实要尝试其他模型，请选择那些专门为结构化推理和工具使用而设计的模型。
:::

5. 点击“开始吧！”来保存你的设置并开始使用 Roo Code
