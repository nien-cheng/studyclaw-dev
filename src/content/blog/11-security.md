---
title: '安全使用 OpenClaw：这些坑一定要避开'
description: 'API Key 泄露、权限过大、网络攻击……这篇讲清楚 OpenClaw 的安全风险，以及怎么安全地使用它。'
pubDate: '2026-05-11'
series: 'advanced'
seriesOrder: 2
seriesLabel: '🏗 进阶应用'
heroImage: '../../assets/blog-placeholder-1.jpg'
---

# 安全使用 OpenClaw：这些坑一定要避开

OpenClaw 是一个本地运行的工具，理论上数据都在你自己的机器上——但这不意味着它绝对安全。

早期版本曾经爆出过多个低成本高危漏洞，虽然都已修复，但了解这些风险点很有必要。

## 主要风险

### 1. API Key 泄露

**风险等级：🔴 极高**

你的模型 API Key（OpenAI / Claude / MiniMax 等）相当于你的账号密码。一旦泄露：
- 别人可以用你的 Key 跑模型，消耗你的配额
- 如果是付费账号，直接扣你的钱

**正确做法：**
- **不要把 API Key 写进配置文件提交到 Git**
- 使用环境变量或 OpenClaw 的 `secrets` 管理
- 定期检查用量是否有异常

### 2. Gateway 端口暴露

**风险等级：🟠 高**

OpenClaw Gateway 默认监听 `127.0.0.1:18789`，这是本地端口。

但如果你的服务器有公网 IP，且 Gateway 端口对公网开放——**任何人都可以直接访问你的 OpenClaw**，无需认证。

**正确做法：**
- 不要让 Gateway 端口暴露在公网
- 如果需要远程访问，用 VPN 或 SSH 隧道
- 启用 Gateway 认证（`gateway.auth` 配置）

### 3. 命令执行权限

**风险等级：🟠 高**

OpenClaw 可以执行系统命令——这意味着如果有人控制了你的 AI，它可以执行任意代码。

**正确做法：**
- 配置命令白名单（`commands.allowlist`）
- 敏感命令（如 `rm`、`sudo`）设置审批流程
- 在 SOUL.md 里明确 AI 的执行边界

### 4. Channel 劫持

**风险等级：🟡 中**

如果有人拿到了你的飞书/Telegram Bot Token，他们可以：
- 冒充你的 Bot 发消息
- 监听你与 AI 的对话

**正确做法：**
- Bot Token 当作密码看待，不要泄露
- 定期更换 Token

## 安全配置参考

```json
{
  "gateway": {
    "port": 18789,
    "auth": {
      "enabled": true,
      "token": "你的随机Token"  // 访问 WebUI 需要这个 Token
    },
    "accessControl": {
      "allowlist": ["127.0.0.1", "你的IP"]
    }
  },
  "commands": {
    "allowlist": ["node", "python", "git"],
    "requireApproval": ["rm", "sudo", "curl"]
  }
}
```

## 开发环境 vs 生产环境

| | 开发环境 | 生产环境 |
|--|---------|---------|
| API Key | 可以用免费额度 | 建议用独立账号 |
| Gateway | 本地访问 | 加认证 + IP 白名单 |
| 日志 | 详细 | 脱敏后保留 |
| Channel Token | 测试 Bot | 独立 Bot，不要和生产混用 |

## 安全检查清单

```
✅ API Key 不写入配置文件（用环境变量）
✅ Gateway 不对公网开放
✅ 启用 Gateway 认证
✅ 配置命令白名单
✅ 敏感命令需要审批
✅ 飞书/Telegram Bot Token 保密
✅ 定期检查用量异常
✅ 关注 OpenClaw 安全公告，及时更新版本
```

## 怎么更新到最新版本？

```bash
npm install -g openclaw@latest
openclaw --version  # 确认版本
```

---

## 小结

OpenClaw 很强大，但**能力越大，风险也越大**。作为可以执行命令、接入你的账号的 AI 工具，安全配置不是可选项，是必选项。

**核心原则：最小权限 + 密钥不外泄 + 访问可控。**

---

*StudyClaw.dev — OpenClaw 中文教程*
