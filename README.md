# 🛡️ TG-AI-Guard: 五擎并发全自动 Telegram 防卫机器人

基于 **Cloudflare Workers** 打造的 Serverless Telegram 社群管理机器人。独创 **“OpenRouter + Cloudflare Workers AI” 五擎并发架构**，实现对群组内各类黑灰产引流、机场推广、软文广告的“降维打击”。

![License](https://img.shields.io/badge/License-MIT-blue.svg)
![Platform](https://img.shields.io/badge/Platform-Cloudflare%20Workers-F6821F.svg)
![AI](https://img.shields.io/badge/AI-Gemma%20%7C%20GLM%20%7C%20Llama-brightgreen.svg)

## ✨ 核心特性

- 🚀 **Serverless 零成本部署**：完美适配 Cloudflare Workers，无需服务器，全球边缘节点低延迟响应。
- 🧠 **究极五擎并发机制**：
  - 支持挂载 **2 个 OpenRouter 节点**与 **3 个 Cloudflare 边缘节点**（原生兼容新一代 Gemma, GLM 等模型）。
  - 五大模型同时推理，任意一个模型判定违规即刻执行拦截（宁可错杀，不可放过）。
- 🎛️ **毫秒级引擎动态开关**：
  - 独家支持 `#` 号快捷禁用语法。只需在代码里给模型名称前加一个 `#`，即可瞬间切断该节点的 API 请求，省钱省力。
- ⚡ **分层漏斗式防御**：
  - **L0 规则直杀**：强正则匹配，瞬间秒杀带 URL、隐藏链接、频道转发的低级推广。
  - **L1 语义透视**：提取特征后交由五大 AI 引擎深度审查，精准打击“求赞”、“机场节点”、“私聊引流”等隐蔽软广。
- ⚖️ **防误伤与自愈闭环**：
  - 支持用户通过点击内联按钮或私聊 `/unban` 实现自动化自助解封，极大降低群主售后成本。
  - 内置隐藏指令 `/resetwebhook`，一键修复 TG 消息断流与 Webhook 掉线异常。

## 📦 快速部署

### 1. 准备工作
- 申请一个 Telegram Bot Token ([@BotFather](https://t.me/BotFather))。
- 准备一个 [Cloudflare](https://dash.cloudflare.com/) 账号，并在控制台获取您的 `Account ID` 和拥有 Workers AI 权限的 `API Token`。
- （可选）准备 [OpenRouter](https://openrouter.ai/) 的 API Key。

### 2. 部署到 Cloudflare Workers
1. 登录 Cloudflare 控制台，进入 **Workers & Pages** -> **Create Worker**。
2. 命名并点击 **Deploy**。随后点击 **Edit Code**。
3. 复制本项目 `worker.js` 中的全部代码并覆盖现有内容。
4. 修改代码顶部的**核心配置区**，填入您的真实 Token：
   ```javascript
   const TG_TOKEN = 'YOUR_TG_TOKEN'; 
   const OPENROUTER_KEY = 'YOUR_OPENROUTER_KEY_1'; 
   const CF_ACCOUNT_ID = 'YOUR_CF_ACCOUNT_ID';
   const CF_API_TOKEN = 'YOUR_CF_API_TOKEN';
