# Awesome Prompts Vault

> 一个精选的**提示词金库** —— 系统提示、编码提示、Agent/工具编排提示，以及原创作品，按可研究、可复用的方式组织，而不是单纯复制粘贴。

[![License: CC BY 4.0](https://img.shields.io/badge/License-CC%20BY%204.0-lightgrey.svg)](./LICENSE)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](./CONTRIBUTING.md)
[![Prompts](https://img.shields.io/badge/prompts-3-orange.svg)](#分类目录)

**简体中文** · [English](./README.en.md)

---

## 为什么是"金库"而不是"清单"

大多数 prompt 仓库是一堆扫一眼就走的文本。这里把每条 prompt 当作**研究过的素材**：**每一份 prompt 都是一个独立目录**，目录下有一份 `README.md`（简介 + 使用说明 + 拆解 + 来源），提炼出**可复用的技巧** —— 分层结构、硬约束前置、能力边界显式声明 —— 让你学到手艺，而不只是抄一份。

```
prompts/<分类>/<slug>/
├── README.md          # 简介 + 使用说明 + 拆解 + 来源（带 frontmatter）
└── <slug>.txt         # 可选：原文（>5000 字符时单独存档，README 保持轻量）
```

## 分类目录

| 分类 | 放什么 | 数量 |
| --- | --- | --- |
| [`system-prompts/`](./prompts/system-prompts/) | 完整系统提示，按来源（anthropic / openai / google / community） | **1** |
| [`coding/`](./prompts/coding/) | 代码生成、审查、重构 | **1** |
| [`agent/`](./prompts/agent/) | Agent 循环、工具定义、多 agent 编排 | **1** |
| [`creative/`](./prompts/creative/) | 写作、设计、创意 | _0_ |
| [`mine/`](./prompts/mine/) | 原创与改造版 | _0_ |

> 数量随条目落地更新。每个分类目录有自己的索引 README。

### 🔥 精选

- **[Claude Fable 5 系统提示（提取版）](./prompts/system-prompts/anthropic/claude-fable-5/)** —— 网传"破解版"的真相辨析 + 122,750 字符原文 + 结构拆解。读懂前沿模型怎么写系统提示。
- **[Loop Engineering 循环工程章程](./prompts/agent/loop-engineering-charter/)** —— 让 Claude 自循环干到完工的可粘贴 charter + `/goal` `/loop` 用法。停止当那个"循环里的人"。
- **[CLAUDE.md 编码六条铁律](./prompts/coding/llm-coding-rules-claude-md/)** —— 用命令式硬规则约束 AI 写代码的可预测错误，含正反代码对照。

## 每条笔记的结构

从 [`templates/PROMPT.template.md`](./templates/PROMPT.template.md) 起步：

```yaml
---
name: ...
prompt_type: system-prompt | coding | agent | creative
source_org: anthropic | openai | google | community | mine
use_case: [agent, design, ...]
model: ...
status: captured | refined | original
source_variant: leaked        # 仅用于提取/泄露版
---
```

**`## 拆解` 是每条笔记的灵魂** —— 至少 3–5 条可复用技巧，不是复述 prompt 说了啥。

## 关于提取版提示词

部分条目是第三方公开的**提取版 / 泄露版**系统提示，收录用于**研究**（安全设计、工具定义、prompt 结构）。它们不是越狱工具，也不解锁任何东西，标 `source_variant: leaked` 并注明来源。若你是内容版权方希望移除，请提 issue。

## 贡献

见 [CONTRIBUTING.md](./CONTRIBUTING.md)：一条 prompt 一篇笔记，真实 frontmatter，拆解要教到东西。

## 致谢

受更广泛的 prompt 工程与系统提示研究社区启发，逐条注明来源。

## 出品与维护

由 **[Onevium](https://github.com/Onevium/Onevium)** 整理维护。Onevium 是一款由 Claude Code 驱动的个人 AI 超级桌面端 —— 自动化浏览器、定时任务、部署 bot，全部集成在一个桌面应用里。觉得这个金库有用，欢迎顺手去 [Onevium](https://onevium.com) 看看，给个 ⭐。

## Star History

[![Star History Chart](https://api.star-history.com/svg?repos=Onevium/awesome-prompts-vault&type=Date)](https://star-history.com/#Onevium/awesome-prompts-vault&Date)

## 协议

内容采用 [CC BY 4.0](./LICENSE) © 2026 onevium.dev —— 署名后自由复用。
