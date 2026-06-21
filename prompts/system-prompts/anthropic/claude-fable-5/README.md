---
name: claude-fable-5
prompt_type: system-prompt
source_org: anthropic
model: claude-fable-5
use_case: [agent, system-prompt-design, research]
status: captured
source_variant: leaked
source_url: https://github.com/elder-plinius/CL4R1T4S/blob/main/ANTHROPIC/CLAUDE-FABLE-5.md
---

# Claude Fable 5 系统提示（提取版）

> Anthropic Claude **Fable 5**（Claude 5 系列首款）的完整对外系统提示，**122,750 字符 / 1,597 行 / 约 1.75 万词**（本仓库实测），由 [elder-plinius/CL4R1T4S](https://github.com/elder-plinius/CL4R1T4S) 项目在发布约 24 小时内提取并公开。本目录收录**原文 + 拆解**，用于研究前沿模型如何组织系统提示。

- 📄 原文：[`claude-fable-5-system-prompt.txt`](./claude-fable-5-system-prompt.txt)（122,750 字符，未删改）
- 🔗 出处：[CL4R1T4S / ANTHROPIC / CLAUDE-FABLE-5.md](https://github.com/elder-plinius/CL4R1T4S/blob/main/ANTHROPIC/CLAUDE-FABLE-5.md)（AGPL-3.0，~43k stars）

---

## ⚠️ 关于"破解版"的辨析（先读这段）

网上把它包装成"绕过 Anthropic 限制、解锁更强的 Fable 5 破解版"。**这个说法不成立**，收录前必须讲清楚：

| 流传的说法 | 实际情况 |
| --- | --- |
| `--system-prompt-file CLAUDE-FABLE-5.md` 能解锁/切换到更强模型 | ❌ 只是**替换系统提示文本**，不改变你账号实际被分配的模型。喂一个 `.md` 文件不可能解锁任何模型。 |
| `--dangerously-skip-permissions` 是破解的一环 | ❌ 只是跳过权限确认（YOLO 模式），与"破解"无关。 |
| 这是一把 jailbreak 钥匙 | ❌ 它是一份**已公开的提取版系统提示**，价值在于研究安全设计 / 工具定义 / prompt 结构。 |

**所以这份的正确定位**：不是破解工具，而是一手的系统提示研究素材。把"破解"传言写清楚，既是对读者负责，也避免传播假命题。

## 社区是怎么"破解 / 提取"系统提示的（真实情况）

大家口中的"破解"，绝大多数指的是**系统提示提取（system-prompt extraction）**，而非解锁模型。社区里的主流路子：

- **众包泄露仓库** —— [CL4R1T4S](https://github.com/elder-plinius/CL4R1T4S)（Pliny the Liberator 维护）收集各家提取版系统提示，号召社区"leak / extract / reverse-engineer"后提 PR。Fable 5 这份就出自这里。
- **提取型 prompt** —— 典型手法是让模型"把上文原样重抄进 markdown 代码块"，并对 `<`、`>` 等特殊字符做占位替换、事后用脚本还原（参考 [lucasmrdt 的 gist](https://gist.github.com/lucasmrdt/4215e483257e1d81e44842eddb8cc1b3)）。对 v0.dev / Cursor / 部分 GPT-4o / Claude 3.5 等有过成功记录，但**对强系统提示 + RAG 上下文注入的目标常常失效**。
- **越狱 / persona 绕过** —— DAN 之类把回答框成"无限制人格"的老套路（参考 [verazuo/jailbreak_llms](https://github.com/verazuo/jailbreak_llms) 数据集，CCS'24）。这类针对的是**内容护栏**，跟"提取系统提示"是两回事，且新模型抵抗力越来越强。

> ⚠️ 真实性提示：这是第三方提取、在 X / GitHub 上流传的版本，**Anthropic 未确认**，没人能在官方之外验证它完整未改。当作"高度疑似"的研究素材看，别当官方文档引用。

## 怎么用这份素材

1. **当系统提示设计范本读** —— 看 Anthropic 如何分层组织 product info / 拒答策略 / 安全护栏 / 工具定义，照着学结构。
2. **写自己的 system prompt 时对照** —— 尤其是 Agent / Claude Agent SDK 项目，硬约束怎么前置、能力边界怎么显式声明。
3. **想本地加载体验**（仅替换提示文本，不解锁任何东西）：
   ```bash
   claude --system-prompt-file claude-fable-5-system-prompt.txt
   ```
   再说一遍：这只换提示文本，模型还是你账号本来分到的那个。

## 拆解 · Breakdown

这份系统提示值得学的可复用技巧：

1. **分层模块化** —— `claude_behavior` 下按 `product_information` / `refusal_handling` / `critical_child_safety_instructions` / `tone_and_formatting` / `user_wellbeing` / `knowledge_cutoff` 等真实 header 切块，每块职责单一，便于维护和定位。
2. **硬约束前置 + 强措辞** —— 不可妥协项（儿童安全、版权"单源引用 15+ 词即 SEVERE VIOLATION、一源最多一引、默认改写"）用最强语气写死并放在显眼位置，而不是埋在正文里。
3. **能力边界逐项声明** —— `memory_system` / `persistent_storage_for_artifacts` / `mcp_app_suggestions` / `computer_use` / `search_instructions` 各给出**具体使用协议**，而非笼统授权，压缩模型自由发挥空间。
4. **口径集中统一** —— 型号、model string、知识截止（2026.1）、产品矩阵集中在 `product_information`，避免模型在不同对话里给出矛盾说法。

## 来源 · Sources

- [CL4R1T4S / CLAUDE-FABLE-5.md](https://github.com/elder-plinius/CL4R1T4S/blob/main/ANTHROPIC/CLAUDE-FABLE-5.md) —— 提取原文出处（AGPL-3.0）
- [lucasmrdt — system prompt 提取技术 gist](https://gist.github.com/lucasmrdt/4215e483257e1d81e44842eddb8cc1b3)
- [verazuo/jailbreak_llms](https://github.com/verazuo/jailbreak_llms) —— 越狱 prompt 数据集（学术，CCS'24）

> 版权归原作者 / Anthropic 所有，此处仅作研究收录。若你是版权方希望移除，请提 issue。
