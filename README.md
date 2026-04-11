# 🛡️ TG-AI-Guard: Serverless 终极群组防卫系统

基于 **Cloudflare Workers** 打造的纯无状态（Stateless）、零数据库依赖的 Telegram 社群管理机器人。独创 **“OpenRouter + CF Workers AI” 五擎并发架构**，结合严密的立体防御网，实现对黑灰产、机场推广、软广引流的“降维打击”。

![License](https://img.shields.io/badge/License-MIT-blue.svg)
![Platform](https://img.shields.io/badge/Platform-Cloudflare%20Workers-F6821F.svg)
![AI](https://img.shields.io/badge/AI-Gemma%20%7C%20GLM%20%7C%20Llama-brightgreen.svg)

## ✨ 核心特性：三维立体防御网

本项目抛弃了笨重的数据库，采用极致轻量的策略组合，将所有防护逻辑压缩在一个脚本内：

### 🧱 1. 城墙防御：新兵隔离营 (Silence Period)
针对“进群秒发广告”、“发黄图跑路”的机器小号：
- 新进群用户在头 **24 小时**内，被系统锁定权限。
- **禁止发送：** 任何外部链接、转发消息、图片、视频及贴纸。仅允许发送纯文本。
- 极大拉高黑灰产养号与引流的转化成本。

### 🧠 2. 重炮防御：五擎并发 AI 审判 (Multi-Engine AI)
针对伪装得极好的“软广”、“心得体会”：
- 支持挂载 **2 个 OpenRouter 节点**与 **3 个 Cloudflare 边缘节点**（原生兼容新一代 Gemma, GLM, Llama 等模型）。
- 过滤机制触发时，五大模型同时进行语义推理，任意一个判定违规即刻执行删帖禁言。
- 🎛️ **内置 `#` 号无损开关**：在模型配置处加 `#` 号即可瞬间停用该节点 API 请求，省钱且方便调试。

### ⚔️ 3. 兜底捕杀：群众路线与特种清剿 (Report & Kill)
针对 AI 难以识别的语音、火星文或图片广告：
- **群众举报**：群友回复可疑消息并发送 `/report` 或 `@admin`，系统会立刻发出高危警告通知管理员跟进。
- **一键斩杀**：管理员发现漏网之鱼，只需回复该消息发送 `/spam` 或 `/kill`，机器人将瞬间**自动删帖、删除指令并彻底禁言该用户**，还群聊以清爽。

## 📦 快速部署指南

### 1. 准备工作
- 申请一个 Telegram Bot Token ([@BotFather](https://t.me/BotFather))。
- 准备一个 [Cloudflare](https://dash.cloudflare.com/) 账号，并在控制台获取您的 `Account ID` 和拥有 Workers AI 权限的 `API Token`。
- （可选）准备 [OpenRouter](https://openrouter.ai/) 的 API Key。

### 2. 部署到 Cloudflare Workers
1. 登录 Cloudflare 控制台，进入 **Workers & Pages** -> **Create Worker**。
2. 命名并点击 **Deploy**。随后点击 **Edit Code**。
3. 复制本项目 `worker.js` 中的全部代码并覆盖现有内容。
4. 修改代码顶部的**核心硬编码配置区**，填入您的真实 Token。
5. 点击 **Deploy** 保存。

### 3. 激活 Webhook（极其关键）
在 TG 中找到您创建的机器人，直接向它发送私聊指令：
`/resetwebhook`
机器人回复“✅ Webhook 权限已强制重置”即代表部署与对接完成。将机器人拉入群组，并赋予其 **删除消息** 和 **封禁/限制用户** 的管理员权限即可生效。

## 💡 AI 引擎动态管理说明

系统内置了优雅的“功能开关（Feature Toggle）”。在配置区，您可以通过在模型名字前添加 `#` 号来临时阻断该节点的网络请求：

```javascript
// 正常启用 Gemma 节点
const CF_AI_MODEL_2 = '@cf/google/gemma-4-26b-a4b-it'; 

// 🛑 临时停用 Kimi 节点 (首字符加 # 即可，不消耗额度，不会引发报错)
const CF_AI_MODEL_1 = '#@cf/moonshotai/kimi-k2.5';
