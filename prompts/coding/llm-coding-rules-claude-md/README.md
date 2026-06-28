---
name: llm-coding-rules-claude-md
prompt_type: coding
source_org: community
use_case: [coding, code-review, agent, claude-code]
model: 任意编码 Agent（Claude Code / Cursor / Copilot 等）
status: captured
source_url: https://drive.google.com/file/d/1mtJKbu-QRk62WTWkyc0M0pGXbKzisA5W/view
---

# CLAUDE.md —— LLM 编码六条铁律

> 一份直接放进项目根目录的 `CLAUDE.md`（也可用作 `.cursorrules` / 系统提示片段），用**命令式硬规则**约束 AI 写代码时反复犯的可预测错误。核心立场：**这些不是建议，是规则** —— 跟着做，产出的代码不用返工；不跟，产出的代码"看着唬人、上线就崩"。

- 📄 原文：[`llm-coding-rules-claude-md.txt`](./llm-coding-rules-claude-md.txt)（完整六节，含正反代码对照）
- 🔗 出处：公开分享的 Google Drive 文档（作者未署名，见文末）
- 🔁 配套：和 [`agent/loop-engineering-charter`](../../agent/loop-engineering-charter/) 同源思路 —— 一个管"单次写代码的纪律"，一个管"让 Agent 自循环干活"。

## 怎么用

1. **整篇放进项目根目录 `CLAUDE.md`**（Claude Code 会自动读取）；Cursor 用户可改名 `.cursorrules`，其他工具粘进系统提示。
2. 按你项目的栈**微调措辞**（如把 `var`/4 空格那类例子换成你项目真实约定），但**保留命令式语气**——铁律的威力来自"不可妥协"的写法，而非礼貌建议。
3. 重点保留每节末尾的**自检问句**（"你能为每一行改动找到与需求的直接联系吗？"），它把抽象原则变成可当场验证的动作。

## 拆解 · Breakdown

值得复用的写法技巧（不是复述规则内容）：

1. **"规则不是建议"的措辞框架** —— 开篇一句 "These are not suggestions. These are rules." 把整份文档的语气钉死。LLM 对**强模态动词 + 后果陈述**（跟做→不返工 / 不跟→上线崩）的依从度，远高于"建议你最好……"。约束 Agent 时，先立这个不可妥协的基调。
2. **给每条规则配一个"失败模式"画像** —— 每节都点名具体的翻车场景（"生成的代码正确但像另一个人写的"、"为不可能发生的错误套 try/catch"）。LLM 靠模式匹配工作，**描述要避免的反例**比正面定义更能锚定行为。
3. **正反代码对照（bad / good）** —— 第 3 节用 `EmailService` 抽象类 vs `send_welcome_email()` 一个函数的直接对比，把"过度工程"这种抽象概念落成可对照的代码 diff，比纯文字规训有效得多。
4. **可当场执行的自检问句收尾** —— "把代码给项目外的人看，如果他问'为什么这里要抽象'而答案是'万一以后……'，就是过度设计了"；"看你的 diff，每一行都能和需求挂上钩吗？"。把原则转成**一句可验证的测试**，是让规则真正生效的关键。
5. **不确定就出声，而非脑补** —— 反复出现的元规则："拿不准就说'我没看到 X 的现成模式，要不要照 Y 来？'，永远好过默默猜。" 显式授权 Agent 暴露不确定性，直接压制"自信地编造"这一最危险失效。
6. **目标驱动 + 先列计划再执行** —— 第 6 节要求把模糊任务（"加校验"）改写成可验证标准（"邮箱缺失/非法时返回 400 + 报错信息 + 两个测试"），多步任务先给编号 Plan 再动手。把"成功长什么样"前置成硬标准。

## 提示词 · Prompt（节选）

> 完整六节见 [`llm-coding-rules-claude-md.txt`](./llm-coding-rules-claude-md.txt)。下面是开篇定调 + 第 4 节"外科手术式修改"节选。

````
# CLAUDE.md

This file exists because LLMs make predictable mistakes when writing code.
Not random mistakes. The same ones, over and over.

These are not suggestions. These are rules. Follow them and you'll produce
code that doesn't need to be rewritten. Ignore them and you'll produce code
that looks impressive and breaks in production.

## 4. Surgical Changes

When you edit existing code, your diff should be as small as possible.

**Don't touch what you weren't asked to touch.** ... Your job is to fix the bug in function A.
**Match the existing style.** ... Consistency within a file beats your personal preference.
**Clean up after yourself, not after others.** ... only if YOUR change caused it.
**Don't reformat.** ... Reformatting creates massive diffs that hide your actual changes.

The test: look at your diff. Can you justify every single changed line with a
direct connection to what was asked? If any line is there because "while I was
in there I thought I'd..." then revert it.
````

六节速览：① Read Before You Write（先读代码再写）② Think Before You Code（先想假设/权衡再写）③ Simplicity（写最少够用的代码）④ Surgical Changes（改动最小化）⑤ Verification（先写复现测试再修）⑥ Goal-Driven Execution（先定可验证目标再动手）。

## 来源 · Source

- 出处：公开分享的 Google Drive 文档 `CLAUDE.md`（[链接](https://drive.google.com/file/d/1mtJKbu-QRk62WTWkyc0M0pGXbKzisA5W/view)，"知道链接者可查看"）。
- 备注：原作者在文档内未署名，本仓库**未能核实作者身份**，按社区流传素材收录，仅作研究与复用参考。若你是原作者或版权方希望署名/移除，请提 issue。
