🤖 Telegram AI Group Management Bot (AI 增强版)

这是一款基于 Cloudflare Workers 部署的轻量级、响应极快的 Telegram 社群管理机器人。它集成了 OpenRouter (AI) 识别能力，专门用于高精度拦截广告、引流、政治违规及低俗内容，并支持全自动的“自助解封”流程。

🌟 核心功能

    🚫 违规内容秒杀：

        链接拦截：普通成员发送任何形式的网址（http/https/www）将触发直接拦截。

        AI 深度审核：利用 Stepfun 等大模型，精准识别软广、引流（如“求赞”、“助力”）、灰黑产、政治敏感及低俗色情内容。

    🛡️ 智能白名单：

        管理员豁免：群主和管理员发送链接或任何内容均不会被拦截。

        身份兼容：完美兼容“匿名管理员”和“以频道名义发言”的身份识别。

    ⏱️ 阅后即焚警告：机器人发出的警告消息将在 10 秒后自动删除，保持群聊界面整洁。

    🔓 自助解封系统：

        被禁言用户点击警告下方的按钮，跳转私聊即可一键恢复发言权限。

        支持动态多群组，一套代码可以同时服务于无限个群组，无需手动硬编码每个群 ID。

    ☁️ 零成本部署：完全运行在 Cloudflare Workers 上，无需服务器，无需维护数据库。

🚀 快速部署指南

1. 准备工作

    Telegram Bot Token: 通过 @BotFather 创建机器人并获取 Token。

    OpenRouter API Key: 访问 OpenRouter 获取 Key。

2. 部署到 Cloudflare Workers

    登录 Cloudflare Dashboard。

    创建一个新的 Worker。

    将项目中的 index.js 代码全部复制并粘贴到 Worker 编辑器中。

    修改代码顶部的 核心硬编码配置区：
    JavaScript

    const TG_TOKEN = '你的_TELEGRAM_TOKEN';
    const OPENROUTER_KEY = '你的_OPENROUTER_KEY';
    const BOT_USERNAME = '你的_机器人用户名_不带@';
    const DEFAULT_GROUP_ID = '你的_主群组ID';

    点击 Save and Deploy。

3. 设置 Webhook

在浏览器地址栏输入以下网址并回车，完成机器人与 Worker 的绑定：
Plaintext

https://api.telegram.org/bot<你的TOKEN>/setWebhook?url=https://<你的WORKER域名>

4. 机器人设置 (重要)

为了让机器人能够读取消息，必须通过 @BotFather 进行以下设置：

    发送 /mybots -> 选择你的机器人 -> Bot Settings。

    Group Privacy: 设置为 Turn OFF。

    Allow Groups: 设置为 ON。

    将机器人拉入群组并设为管理员，确保赋予“删除消息”和“封禁用户”权限。

🛠️ 配置说明 (SYSTEM_PROMPT)

机器人通过高度优化的提示词进行过滤，你可以根据需求在代码中修改：

    广告引流：拦截返佣、求赞、助力、私聊等行为。

    政治敏感：过滤带节奏、擦边球等话题。

    低俗内容：拦截色情、恋童、血腥内容。

💬 使用指令

    群组中：机器人全自动监控，无需指令。

    私聊中：

        /unban：自助解除主群禁言。

        /unban <群组ID>：通过群组 ID 手动解除特定群组的禁言。

        直接发送 -100xxxxxxx：引导其他群主进行机器人登记。

📄 开源协议

MIT License
