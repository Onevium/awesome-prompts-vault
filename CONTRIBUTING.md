# 贡献指南 · Contributing

> 一条 prompt 一篇笔记，真实 frontmatter，拆解要教到东西。这是金库，不是垃圾场。

## 一条笔记长什么样

**每一份 prompt 都是一个独立目录**，目录下必须有一份 `README.md`（简介 + 使用说明 + 拆解 + 来源）。从 [`templates/PROMPT.template.md`](./templates/PROMPT.template.md) 起步：

```
prompts/<分类>/<slug>/
├── README.md          # 必需：简介 + 使用说明 + 拆解 + 来源（带 frontmatter）
└── <slug>.txt         # 可选：原文（>5000 字符时单独存档，README 保持轻量）
```

## 规则

1. **一条 prompt = 一个目录 + 一份 README.md。** 不要把多条塞进一个文件。
2. **`name`** —— `kebab-case`，仓库内唯一，与目录名一致。
3. **选对分类** —— `system-prompts` / `coding` / `agent` / `creative` / `mine`。系统提示再按来源放进 `anthropic` / `openai` / `google` / `community` 子目录。
4. **`## 拆解` 是硬要求** —— 至少 3–5 条可复用技巧（分层结构、硬约束前置、能力边界声明……），不是复述 prompt 内容。
5. **来源如实标注，不编造。** 抓不到的 star / 出处就留空或 `?`，绝不脑补。
6. **提取版 / 泄露版**必须标 `source_variant: leaked` 并注明第三方来源，仅作研究用途。
7. **不含密钥、私有路径、机密内容。** 提交前清掉绝对家目录路径和凭据。

## frontmatter 契约

```yaml
---
name: my-prompt
prompt_type: system-prompt | coding | agent | creative
source_org: anthropic | openai | google | community | mine
use_case: [agent, design, ...]
model: ...
status: captured | refined | original
source_variant: leaked        # 仅提取/泄露版需要
---
```

`name`、`prompt_type`、`source_org`、`status` 为必填。破坏契约的 PR 不予合并。

## 提交流程

1. Fork → 新建分支 → 加你的笔记。
2. 顺手更新对应分类的索引 README 与数量徽章。
3. 用 PR 模板发起 PR，维护者会做结构与合规检查。

---

> English: one prompt per note, real frontmatter, and a `## Breakdown` that teaches reusable techniques (not a restatement). Tag extracted/leaked prompts with `source_variant: leaked` and credit the source. No secrets or private paths. Start from [`templates/PROMPT.template.md`](./templates/PROMPT.template.md).
