---
title: '多智能体团队：一个 OpenClaw，多个专业助理'
description: 'subagent 是什么？怎么让多个 AI 助手协作？这篇讲清楚 OpenClaw 的多智能体架构，以及怎么搭建你自己的 AI 团队。'
pubDate: '2026-05-11'
series: 'advanced'
seriesOrder: 1
seriesLabel: '🏗 进阶应用'
heroImage: '../../assets/blog-placeholder-5.jpg'
---

# 多智能体团队：多个助手协作

当一个 AI 助手不够用的时候，OpenClaw 支持**多智能体团队**——每个 Agent 各司其职，互相协作。

## 什么场景需要多个 Agent？

| 场景 | 方案 |
|------|------|
| 写作 + 生图 + 股票分析 | 三个专业 Agent 分工 |
| 工作用 + 个人用 | 两个独立 Agent，记忆隔离 |
| 不同项目 | 每个项目一个 Agent，避免记忆混淆 |

## Agent 的基本概念

- **主 Agent（Main）**：默认的 AI 助手，处理日常任务
- **Subagent（子 Agent）**：专门处理特定任务，可以是临时创建，也可以长期存在

## 怎么启动一个子 Agent？

### 临时子 Agent

```bash
openclaw agents spawn --name "写作助手" --task "帮我写文章"
```

这个 Agent 完成任务后自动关闭。

### 长期子 Agent

在配置文件里定义：

```json
{
  "agents": {
    "writing-assistant": {
      "identity": {
        "name": "花园写作助手"
      },
      "model": "claude-sonnet-4-6",
      "skills": ["writing", "tavily-search"]
    }
  }
}
```

## 实际案例：花园多智能体团队

花园老师（ConardLi）搭建了一套自己的 AI 团队：

| Agent | 职责 |
|-------|------|
| 花园智能总管 | 统一入口，理解用户意图，分发任务 |
| 花园生图助手 | 专门处理图片生成 |
| 花园资讯助手 | 每天自动抓取 AI 新闻，生成日报 |
| 花园投资助手 | 监控股票，异动通知 |
| 花园写作助手 | 辅助写文章、润色文案 |
| 花园社区助手 | 管理 GitHub Issue 和社区问答 |

**工作流示例：**

```
用户：帮我写一篇关于 OpenClaw 的推广文章

     ↓
花园智能总管（主 Agent）
     ↓
理解意图 → 分发给"写作助手"
     ↓
写作助手：查资料 + 起草文章
     ↓
如果需要配图 → 分发给"生图助手"
     ↓
汇总结果返回给用户
```

## 多 Agent 的通信机制

OpenClaw 的多 Agent 之间通过**消息总线**通信，每个 Agent 有独立的：
- 会话上下文
- 记忆空间
- 技能配置

这样可以避免"写作的时候被股票信息干扰"的问题。

## 怎么搭建自己的多 Agent 团队？

### 第一步：明确分工

列出你最常做的事，给每类事配一个 Agent。比如：
- 写作 + 润色
- 信息搜索
- 日程管理
- 社交媒体运营

### 第二步：逐个创建

```bash
# 创建写作助手
openclaw agents create writing \
  --soul "./souls/writing.md" \
  --skills "writing,tavily-search"

# 创建资讯助手
openclaw agents create news \
  --soul "./souls/news.md" \
  --cron "0 8 * * *"  # 每天早上自动执行
```

### 第三步：配置主 Agent 分发规则

在主 Agent 的 SOUL.md 里写清楚什么任务分发给谁：

```markdown
## 任务分发规则
- 写文章类 → 交给 writing-assistant
- 图片生成 → 交给 image-assistant
- 股市查询 → 交给 finance-assistant
- 其他 → 我自己处理
```

## 小结

多智能体的核心价值是**专业化分工**——让每个 Agent 做它最擅长的事，比一个通才 Agent 效果更好。

但也不要过度设计，从 2-3 个开始，慢慢扩展。

---

*StudyClaw.dev — OpenClaw 中文教程*
