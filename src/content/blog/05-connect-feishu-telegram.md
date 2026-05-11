---
title: '把 OpenClaw 接起飞书 / Telegram：让它成为你的日常工具'
description: '装好了但没接入任何聊天工具？这一步教你怎么把飞书和 Telegram 接入 OpenClaw，让它真正成为你每天可用的私人助理。'
pubDate: '2026-05-11'
series: 'core-features'
seriesOrder: 1
seriesLabel: '🔧 核心功能'
heroImage: '../../assets/blog-placeholder-5.jpg'
---

# 接起飞书 / Telegram

这一篇的目标：**让 OpenClaw 接入飞书或 Telegram，这样你发一条消息就能和它对话。**

## 方案对比：飞书 vs Telegram

| | 飞书 | Telegram |
|--|------|---------|
| 国内使用 | ✅ 直接用 | ⚠️ 需要科学上网 |
| Bot 创建 | 需要企业账号或企业自建应用 | @BotFather 一键创建 |
| 功能支持 | 完整 | 完整 |
| 配置难度 | 中等 | 简单 |

**推荐国内用户先试飞书，有境外需求选 Telegram。**

---

## 方式一：接入 Telegram（更简单）

### 第一步：创建 Bot

1. 在 Telegram 搜索 **@BotFather**
2. 发送 `/newbot`
3. 给 Bot 起名字（显示名）和用户名（需以 bot 结尾）
4. 拿到一个 **Bot Token**，格式类似：`123456789:ABCdefGhIJKlmNoPQRstuVWXyz`

### 第二步：在 OpenClaw 配置

打开配置文件 `~/.openclaw/openclaw.json`，在 `channels` 里加入：

```json
{
  "channels": {
    "telegram": {
      "enabled": true,
      "botToken": "你的BotToken"
    }
  }
}
```

或者用命令行：

```bash
openclaw channels add telegram --token 你的BotToken
```

### 第三步：重启 Gateway

```bash
openclaw run
```

### 第四步：发消息

在 Telegram 找到你的 Bot，点击"Start"或发一条消息。

如果配置正确，它会立刻回复——**你的 Telegram Bot 已经接好了。**

---

## 方式二：接入飞书（功能更强）

飞书接入稍微复杂一点，但功能也更完整。以下是大致步骤：

### 第一步：创建飞书自建应用

1. 打开 [open.feishu.cn/app](https://open.feishu.cn/app)
2. 点击"创建企业自建应用"
3. 填写应用名称、描述，上传图标
4. 获取 **App ID** 和 **App Secret**

### 第二步：配置权限

在应用后台，开通以下权限：
- `im:message`（读取消息）
- `im:message:send_as_bot`（发送消息）

### 第三步：配置事件订阅

1. 在"事件订阅"中，配置请求地址（URL）
2. 配置加解密密钥

### 第四步：在 OpenClaw 配置

```json
{
  "channels": {
    "feishu": {
      "enabled": true,
      "appId": "你的AppID",
      "appSecret": "你的AppSecret"
    }
  }
}
```

### 第五步：重启并测试

```bash
openclaw run
```

在飞书给 Bot 发一条消息测试。

---

## 常见问题

**Telegram 收不到回复？**
- 确认 Bot Token 正确
- 确认 Gateway 已重启
- 检查防火墙是否开放了 18789 端口

**飞书报错"机器人不在线"？**
- 确认事件订阅的 URL 可公网访问
- 确认加密密钥配置正确

**想同时接入多个平台？**
- 在 channels 配置里同时写入多个平台即可
- OpenClaw 会自动路由到对应的 Bot

---

## 下一步

接好聊天渠道之后，你可以：

- [给它设定人格，让它更像你的私人助理](/blog/06-personality)
- [配置定时任务，让它每天自动给你发资讯](/blog/08-auto-tasks)
- [安装技能，让它能力更强](/blog/09-skills)

---

*StudyClaw.dev — OpenClaw 中文教程*
