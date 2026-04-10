# 🛡️ TG-AI-Guard: 三擎并发全自动 Telegram 社群防卫机器人

基于 **Cloudflare Workers** 无服务器架构打造的 Telegram 极严社群管理机器人。独创 **OpenRouter 双节点 + Cloudflare Workers AI (Kimi 2.5)** 三擎并发架构，实现对 Telegram 群组广告、引流、黑灰产及违规内容“宁可错杀，不可放过”的毫秒级拦截。

![License](https://img.shields.io/badge/License-MIT-blue.svg)
![Platform](https://img.shields.io/badge/Platform-Cloudflare%20Workers-F6821F.svg)
![AI](https://img.shields.io/badge/AI-OpenRouter%20%7C%20Kimi%202.5-brightgreen.svg)

## ✨ 核心特性

* 🚀 **无服务器架构**：原生适配 Cloudflare Workers，零服务器运维成本，全球边缘节点极速响应。
* 🧠 **三擎并发 AI 识别**：
    * **主节点**：OpenRouter 免费/付费模型（如 Nvidia/Llama 等）。
    * **备节点**：OpenRouter 备用模型（如 Stepfun 等）。
    * **边缘节点**：原生调用 Cloudflare Workers AI（接入月之暗面 Kimi 2.5），超低延迟。
    * *只要任意一个 AI 引擎判定违规，即刻执行封禁，确保绝不漏网。*
* ⚡ **双重拦截防线**：
    * **第一道（正则必杀）**：瞬间拦截任何形式的 URL、隐藏链接、频道转发。
    * **第二道（AI 语义透视）**：深度识别“加群”、“求赞”、“机场节点推荐”、“软广引流”及各类违规话题。
* ⚖️ **人性化自助解封**：支持被误伤的用户通过点击按钮或私聊机器人发送 `/unban` 自动恢复权限，极大降低管理员售后成本。
* 🛠️ **自愈能力**：内置 `/resetwebhook` 隐藏指令，一键修复 Telegram Webhook 掉线问题。

## 📦 部署指南 (仅需 3 分钟)

### 1. 准备工作
* 一个 Telegram Bot Token（通过 [@BotFather](https://t.me/BotFather) 获取）。
* 至少一个 [OpenRouter](https://openrouter.ai/) API Key。
* 一个 [Cloudflare](https://dash.cloudflare.com/) 账号，并在控制台获取您的 `Account ID` 和拥有 Workers AI 权限的 `API Token`。

### 2. 部署到 Cloudflare Workers
1. 登录 Cloudflare 控制台，进入 **Workers & Pages**。
2. 点击 **Create Application** -> **Create Worker**，随便起个名字并部署。
3. 点击 **Edit Code**，将本项目 `worker.js` 中的全部代码复制并覆盖进去。
4. 修改代码顶部的**核心硬编码配置区**：

```javascript
// 1. Telegram Bot Token
const TG_TOKEN = 'YOUR_TG_TOKEN'; 

// 2. OpenRouter API Key
const OPENROUTER_KEY = 'YOUR_OPENROUTER_KEY_1'; 
const OPENROUTER_KEY_2 = 'YOUR_OPENROUTER_KEY_2'; // 备用，可留空

// 3. Cloudflare Workers AI 配置
const CF_ACCOUNT_ID = 'YOUR_CF_ACCOUNT_ID';
const CF_API_TOKEN = 'YOUR_CF_API_TOKEN';

// 4. 你的机器人用户名 (非常重要，用于解封跳转)
const BOT_USERNAME = 'your_bot_username';
