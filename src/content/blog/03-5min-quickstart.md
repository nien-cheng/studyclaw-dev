---
title: '5 分钟把 OpenClaw 跑起来：最小闭环，快速体验'
description: '跟着做，零基础也能在 5 分钟内把 OpenClaw 装好、配置好、聊上天。扫除恐惧感，从这里开始。'
pubDate: '2026-05-11'
series: 'getting-started'
seriesOrder: 3
seriesLabel: '🚀 入门启动'
heroImage: '../../assets/blog-placeholder-3.jpg'
---

# 5 分钟把 OpenClaw 跑起来

这一篇目标很明确：**让你在 5 分钟内把 OpenClaw 装好，跑起来，收到第一条 AI 回复。**

不讲大道理，就是动手。

## 你需要准备什么

- 一台电脑（Mac / Windows / Linux 都可以）
- Node.js 22 或以上版本
- 一个大模型的 API Key（可选，先跳过也行）

## 第一步：检查 Node.js

打开终端（Mac 是"终端"App，Windows 是"CMD"或 PowerShell），输入：

```bash
node --version
```

如果显示的是 `v22.x.x` 或更高，Node.js 已经就绪。

如果没装或版本太低，去 [nodejs.org](https://nodejs.org) 下载安装即可（选 LTS 版本）。

## 第二步：一键安装 OpenClaw

在终端输入这一行：

```bash
npm install -g openclaw@latest
```

等待 1-2 分钟安装完成。中间出现的 warning 提示可以忽略。

验证安装成功：

```bash
openclaw --version
```

看到版本号就说明装好了。

## 第三步：初始化配置

运行初始化向导：

```bash
openclaw onboard --install-daemon
```

会弹出几个提示：

1. **安全提示** — 问你当前环境是否安全（没有特殊要求选 Yes）
2. **选择模式** — 选 `QuickStart`（新手推荐）
3. **选择模型** — 如果你有 API Key 可以填入；如果没有可以先 Skip
4. **跳过 Channel** — 先不接平台，后续再配
5. **跳过 Skills** — 先跳过
6. **开启 Hooks** — 建议开启 `command-logger` 和 `session-memory` 两个钩子
7. **完成** — 看到带有 Token 的 WebUI 地址

## 第四步：打开 WebUI，发第一条消息

安装向导结束后，终端会显示一个本地地址，例如：

```
Gateway running on http://localhost:18789
```

在浏览器打开这个地址，你会看到 OpenClaw 的控制台界面。

直接在输入框里发一条消息：

> 你好，你是谁？

如果一切正常，你会收到 AI 的回复——**这就是你的第一个 OpenClaw 对话。**

## 常见问题

**安装卡住不动？**

- 换个网络，或者用手机热点
- 国内用户可以加 `--registry` 参数：`npm install -g openclaw@latest --registry https://registry.npmmirror.com`

**看到 402 或余额不足？**

- 说明模型 API 没配置或余额用完了
- 可以先配置免费模型，或者去 MiniMax/硅基流动等平台申请免费 API Key

**WebUI 打不开？**

- 确认 Gateway 进程在运行
- 试试重新运行 `openclaw run`

## 下一步

恭喜你，最难的部分已经过去了。

现在 OpenClaw 跑起来了，接下来你可以：

- [接起飞书/Telegram，把它变成日常工具](/blog/04-connect-feishu-telegram)
- [了解它的基本概念，理解它是怎么工作的](/blog/04-concepts)
- [给它设定人格，让它更像你的私人助理](/blog/06-personality)

---

*StudyClaw.dev — OpenClaw 中文教程*
