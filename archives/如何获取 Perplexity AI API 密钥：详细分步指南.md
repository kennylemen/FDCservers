# 如何获取 Perplexity AI API 密钥：详细分步指南

Perplexity AI 是一款集搜索引擎与聊天机器人于一体的人工智能工具，通过自然语言处理技术为用户提供即时、准确的网络信息搜索与整合服务。自 2022 年推出以来，Perplexity AI 凭借其卓越的自然语言处理能力和广泛的应用场景，吸引了众多开发者的关注。为了帮助开发者更好地利用这一工具，本文将详细指导如何获取 Perplexity AI API 密钥，并逐步解锁这一技术宝藏，为项目注入全新活力。

## 1. 注册并登录 Perplexity AI



首先，访问 Perplexity AI 官网并完成注册。注册后，使用您的账号登录以继续后续操作。

## 2. 获取 Perplexity AI API 密钥

### 1. 绑定信用卡
在开始使用 API 前，您需要绑定信用卡以完成付款设置。此步骤不会立即扣款，而是存储付款信息以便后续使用。



### 2. 生成 API 密钥
绑定信用卡后，您可以生成 API 密钥。API 密钥是一个长期有效的访问令牌，在手动刷新或删除之前一直可用。



### 3. 配置自动充值（可选）
为了避免信用额度用完导致 API 密钥被禁用，建议配置“自动充值”功能。当信用额度低于 2 美元时，系统会自动刷新余额。

## 3. 使用 API 密钥

在每个 API 请求中，将 API 密钥作为授权标头中的承载令牌发送。以下是一个使用 Perplexity AI API 的示例代码：

python
from openai import OpenAI

YOUR_API_KEY = "INSERT API KEY HERE"

messages = [
    {
        "role": "system",
        "content": (
            "You are an artificial intelligence assistant and you need to "
            "engage in a helpful, detailed, polite conversation with a user."
        ),
    },
    {
        "role": "user",
        "content": "How many stars are in the universe?",
    },
]

client = OpenAI(api_key=YOUR_API_KEY, base_url="https://api.perplexity.ai")

# 非流式聊天完成
response = client.chat.completions.create(
    model="llama-3.1-sonar-large-128k-online",
    messages=messages,
)
print(response)

# 流式聊天完成
response_stream = client.chat.completions.create(
    model="llama-3.1-sonar-large-128k-online",
    messages=messages,
    stream=True,
)
for response in response_stream:
    print(response)


## 4. PerplexityBot 网络爬虫

Perplexity 使用名为 **PerplexityBot** 的网络爬虫从互联网上收集信息，并将其编入搜索引擎索引中。您可以通过以下方式识别或限制 PerplexityBot：

plaintext
User agent token: PerplexityBot
Full user agent: User-Agent: Mozilla/5.0 AppleWebKit/537.36 (KHTML, like Gecko; compatible; PerplexityBot/1.0; +https://perplexity.ai/perplexitybot)


### 禁止 PerplexityBot 访问
若您不希望 PerplexityBot 访问您的网站数据，可以在 `robots.txt` 中添加以下记录：

plaintext
User-Agent: PerplexityBot
Disallow: /


### 自定义访问规则
您还可以通过以下方式自定义 PerplexityBot 的访问权限，例如仅允许其访问特定路径：

plaintext
User-Agent: PerplexityBot
Allow: /public/
Disallow: /private/


## 5. 常见问题

### Q1：如何找到 Perplexity AI API？
A1：您可以通过 Perplexity AI 官方文档或开发者平台获取 API 的相关信息。

### Q2：该 API 目前支持网页浏览吗？
A2：是的！Perplexity Sonar Models 利用了来自 Perplexity 搜索索引和公共互联网的信息。

### Q3：什么是 API-KEY？
A3：API-KEY 是用于调用鉴权和计量计费的密钥，支持主账号进行管理。

### Q4：如何应对 401:授权错误？
A4：401 错误表示 API 密钥无效、已删除或信用不足。您可以通过充值或配置自动充值来解决此问题。

### Q5：Perplexity 是否提供服务质量保证？
A5：目前 Perplexity 不保证服务的正常运行时间、故障频率及恢复时间。

### Q6：API 提交的用户数据是否会用于模型训练？
A6：Perplexity 仅收集可计费的使用元数据和用户账户信息，不会将用户数据用于模型训练。

## 6. 总结

本文详细介绍了获取 Perplexity AI API 密钥的全过程，从注册账号到生成密钥再到实际使用，提供了清晰的分步指南。通过本文，开发者可以轻松解锁 Perplexity AI 的强大功能，并将其集成到应用中，从而提升用户体验和产品功能。

👉 [WildCard | 一分钟注册，轻松订阅海外线上服务](https://bbtdd.com/WildCard)