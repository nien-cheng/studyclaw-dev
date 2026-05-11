---
title: 'Skills 技能系统：让 OpenClaw 能力升级的扩展包'
description: 'ClawHub 是什么？怎么安装技能？一个技能是怎么组成的？这篇讲清楚 OpenClaw 的技能扩展机制。'
pubDate: '2026-05-11'
series: 'core-features'
seriesOrder: 5
seriesLabel: '🔧 核心功能'
heroImage: '../../assets/blog-placeholder-4.jpg'
---

# Skills 技能系统：让 OpenClaw 能力升级

OpenClaw 本身已经很强，但它有一个**技能市场（ClawHub）**，可以让你像装 App 一样给 OpenClaw 增加新能力。

## 什么是 Skills？

Skills 是**结构化的操作手册/执行流程**。

它解决了"大模型不知道何时用、按什么顺序用工具"的问题——Skills 明确规定了特定场景下，工具的使用顺序、执行逻辑、注意事项。

```
MCP 解决的问题：能不能调用某个工具
Skills 解决的问题：什么时候用、怎么用、按什么顺序
```

## ClawHub：技能市场

[ClawHub.ai](https://clawhub.ai) 是 OpenClaw 的官方技能市场，里面有各种社区贡献的技能：

- 🔍 搜索类（Tavily 搜索、实时新闻）
- 📊 数据分析类（股票查询、数据处理）
- 🖼 生图类（图片生成）
- 📅 日历/邮件类
- 🔧 开发类（GitHub 管理、代码调试）
- ...更多

## 怎么安装技能？

### 方式一：用命令行

```bash
openclaw skills install tavily-search
openclaw skills install weather
openclaw skills install github
```

### 方式二：用 OpenClaw WebUI

1. 打开控制台（`openclaw run` 的 WebUI 地址）
2. 进入 Skills 页面
3. 搜索想要的技能，点安装

### 方式三：从 ClawHub 网站找安装命令

1. 打开 [clawhub.ai](https://clawhub.ai)
2. 找到想要的技能
3. 复制安装命令

## 热门技能推荐

### Tavily Search（搜索）
```bash
openclaw skills install tavily-search
```
让 OpenClaw 能够搜索实时网络信息，告别"我的知识截止到XX月"。

### Weather（天气）
```bash
openclaw skills install weather
```
查天气预报——"明天去北京，带什么衣服？"

### GitHub（代码管理）
```bash
openclaw skills install github
```
帮你管 GitHub：查 Issue、PR 状态、创建里程碑。

### Feishu Calendar（飞书日历）
```bash
openclaw skills install feishu-calendar
```
直接读写飞书日历，帮你安排会议。

## 技能是怎么组成的？

一个技能通常包含：

```
skill-name/
├── SKILL.md          # 技能说明书
├── scripts/          # 脚本文件
│   └── search.mjs    # 实际执行的脚本
└── README.md         # 使用说明
```

`SKILL.md` 是核心——它告诉 OpenClaw：
- 这个技能是什么、什么时候用
- 需要哪些环境变量（API Key 等）
- 怎么调用它的脚本
- 使用示例

## 注意事项

1. **API Key**：很多技能需要额外的 API Key（比如 Tavily 需要申请免费 Key）
2. **按需安装**：不要一次装太多，技能越多调用越不稳定
3. **查看日志**：如果技能不工作，`openclaw logs` 查一下错误

## 小结

| | 说明 |
|---|------|
| Skills | 结构化的操作流程，让 AI 知道何时用、怎么用工具 |
| ClawHub | 技能市场，里面有社区贡献的各种技能 |
| 安装方式 | 命令行 / WebUI / 从网站复制命令 |
| 热门推荐 | tavily-search、weather、github、feishu-calendar |

---

*StudyClaw.dev — OpenClaw 中文教程*
