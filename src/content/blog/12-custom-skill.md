---
title: '开发自己的 Skill：让 OpenClaw 做任何你想要的事'
description: 'ClawHub 上的技能不够用？想自己写一个？这篇手把手教你从零开发一个 OpenClaw Skill，包含 SKILL.md 怎么写、脚本怎么调。'
pubDate: '2026-05-11'
series: 'advanced'
seriesOrder: 3
seriesLabel: '🏗 进阶应用'
heroImage: '../../assets/blog-placeholder-2.jpg'
---

# 开发自己的 Skill

ClawHub 上的技能很多，但不是每个都符合你的需求。这篇教你**从零开发一个自己的 Skill**。

## Skill 的基本结构

```
my-custom-skill/
├── SKILL.md          # 技能说明书（必需）
├── scripts/          # 执行脚本
│   └── run.mjs       # 主脚本
├── README.md         # 使用文档（可选）
└── package.json      # 依赖（可选）
```

## 第一步：创建 SKILL.md

这是 Skill 的核心，它告诉 OpenClaw：
- 这个 Skill 是什么
- 什么时候用
- 需要哪些环境变量
- 怎么调用

```markdown
# SKILL.md

## 名称
my-custom-skill

## 描述
帮我查快递物流信息，支持顺丰/中通/圆通

## 触发词
查快递、物流追踪

## 所需环境变量
- `EXPRESS_API_KEY`：快递100 API Key（免费申请）

## 执行脚本
scripts/track.mjs

## 使用示例
"帮我查一下快递 1234567890"
```

## 第二步：写执行脚本

`scripts/track.mjs`：

```javascript
#!/usr/bin/env node

// 从参数获取快递单号
const trackingNumber = process.argv[2];

if (!trackingNumber) {
  console.log("请提供快递单号，例如：openclaw skills run my-custom-skill 1234567890");
  process.exit(1);
}

// 调用快递 API（这里用快递100示例）
const response = await fetch(`https://api.kuaidi100.com/api?id=YOUR_KEY&com=yto&nu=${trackingNumber}`);
const data = await response.json();

console.log(`📦 快递单号：${trackingNumber}`);
console.log(`📍 最新状态：${data.lastStatus}`);
console.log(`⏰ 更新时间：${data.lastTime}`);

// 返回给 OpenClaw
console.log("::OPENCLAW_RESULT::", JSON.stringify(data));
```

## 第三步：安装 Skill

```bash
openclaw skills install ./my-custom-skill
```

或者打包发布到 ClawHub，让别人也能用：

```bash
openclaw skills publish ./my-custom-skill
```

## 实际案例：花园生图助手

花园老师开发的生图助手是一个 Skill：

```markdown
# 花园生图助手 SKILL.md

## 触发词
生图、图片生成、画一张图

## 执行脚本
scripts/image.mjs

## 所需环境变量
- `OPENAI_API_KEY`：GPT-4o 的 API Key
```

它的 `image.mjs` 会调用 DALL-E 或 FLUX API 生成图片，返回给你。

## Skill 开发的几个 Tips

### 1. 先想清楚触发条件
不要让 Skill 太宽泛——"帮我"什么都触发不了。

### 2. 错误处理要做好
网络可能失败，API 可能报错，做好 `try-catch` 和友好的错误提示。

### 3. 结果格式要统一
用 `::OPENCLAW_RESULT::` 前缀返回结构化数据，OpenClaw 更容易解析。

### 4. 参考已有的 Skill
去 [clawhub.ai](https://clawhub.ai) 找类似功能的 Skill 源码参考。

## 小结

开发 Skill 的三步：
1. 写 `SKILL.md`（告诉 AI 什么时候用、怎么调用）
2. 写 `scripts/*.mjs`（实际执行逻辑）
3. 用 `openclaw skills install` 安装

**Skill 是 OpenClaw 的能力边界——你能写出什么样的 Skill，它就能做什么样的事。**

---

*StudyClaw.dev — OpenClaw 中文教程*
