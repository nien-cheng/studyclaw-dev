---
title: 'OpenClaw 核心概念：Gateway / Channel / Memory / Agent 全解析'
description: 'Gateway、Channel、Memory、Agent……这些 OpenClaw 的核心概念到底是干什么的？这篇用大白话讲清楚。'
pubDate: '2026-05-11'
series: 'getting-started'
seriesOrder: 4
seriesLabel: '🚀 入门启动'
heroImage: '../../assets/blog-placeholder-4.jpg'
---

# OpenClaw 核心概念解析

跑起来之后，你可能会好奇：OpenClaw 内部是怎么运转的？这篇把几个核心概念逐个讲清楚。

## 整体架构：像一个 AI 操作系统

OpenClaw 采用的是**"微核 + 插件 + 统一网关"**的架构模式，可以理解为一个**AI 操作系统**。

消息从各个聊天渠道进来 → 经过 Gateway 调度 → 交给 Agent 处理 → 返回结果。

```
微信 / 飞书 / Telegram / ...
         │
         ▼
      Gateway（网关）
         │
         ├── 调度任务
         ├── 管理记忆
         ├── 执行定时任务
         └── 控制工具调用
```

## Gateway（网关）

**Gateway 是整个系统的心脏。**

它不做"思考"——思考交给 Agent。它做的是：
- 接收所有渠道的消息
- 判断交给哪个 Agent 处理
- 管理会话状态
- 调度定时任务
- 控制工具调用

可以把它理解为一个**电话总机**——所有渠道的消息进来，它负责转接给合适的人处理。

## Channel（渠道）

**Channel 是 OpenClaw 和各种聊天平台的适配器。**

OpenClaw 支持同时连接 20+ 个平台：

- 飞书
- Telegram
- Discord
- WhatsApp
- Slack
- 企业微信
- Signal
- ...更多

每个平台有自己的适配器（Channel），但体验完全一致——你在微信说的和 Telegram 说的，Agent 感受到的是一样的上下文。

## Memory（记忆系统）

这是 OpenClaw 最特别的部分——**分层记忆架构**。

| 层级 | 文件 | 作用 |
|------|------|------|
| 身份层 | SOUL.md | 定义 AI 的性格、语调、行为边界 |
| 用户层 | USER.md | 记录用户的个人资料和偏好 |
| 操作层 | AGENTS.md | 操作指南、工作流程、能力边界 |
| 索引层 | MEMORY.md | 核心信息索引（保持精简） |
| 日志层 | memory/日期.md | 每日原始记录 |

**举个小例子：**

你跟它说"按老样子来"——它会理解你说的"老样子"是什么意思，因为它记得你之前的偏好。

这就是为什么用得越久，它越懂你。**复利效应。**

## Agent（智能体）

**Agent 是帮你执行任务的 AI 实体。**

一个完整的 Agent 同时具备：
- **Memory**：记忆上下文
- **RAG**：调用外部知识
- **MCP**：调用外部工具
- **Skills**：特定场景的执行流程

你可以理解为：Agent = 大脑（模型）+ 记忆 + 工具箱 + 操作手册。

## Hooks（扩展机制）

Hooks 允许你在 OpenClaw 的运行周期内，**拦截系统事件并触发自定义逻辑**。

比如：
- 用户执行了某个命令 → 记录日志
- 开始新会话 → 保存之前的状态
- 执行出错 → 发送通知

## CronJob（定时任务）

这是 OpenClaw 从"被动响应"变成"主动出击"的关键。

你设置一个定时规则（比如每天早上 8 点），OpenClaw 会在后台自动唤醒，执行既定工作——比如给你发一份今日日程、监控的股票早报、新闻摘要。

**不需要你发消息，它自己会动。**

## 这些概念怎么配合？

```
用户发消息（Telegram/飞书/...）
    │
    ▼
Gateway 接收消息
    │
    ├── 查看用户 Memory（了解背景）
    │
    ├── 调度给 Agent
    │       │
    │       ├── 加载 SOUL.md（人格设定）
    │       ├── 读取 USER.md（用户偏好）
    │       ├── 调用工具（Tools via MCP）
    │       └── 执行 Skills（流程）
    │
    └── 返回结果给用户
```

---

## 小结

| 概念 | 作用 |
|------|------|
| Gateway | 系统中枢，消息路由和调度 |
| Channel | 连接各种聊天平台的适配器 |
| Memory | 分层记忆，让 AI 越用越懂你 |
| Agent | 执行任务的 AI 实体 |
| Hooks | 生命周期事件扩展 |
| CronJob | 主动定时执行任务 |

**下一篇预告：** 《接起飞书/Telegram》，把 OpenClaw 变成你每天真正在用的工具。

---

*StudyClaw.dev — OpenClaw 中文教程*
