---
name: loop-engineering-charter
prompt_type: agent
source_org: community
use_case: [agent, automation, workflow, claude-code]
model: Claude Code（/goal、/loop 命令）
status: captured
source_url: https://x.com/Raytar/status/2069212188619805179
---

# Loop Engineering 循环工程章程

> 把"你盯着 AI 一步步干活"变成"AI 自己循环干到完工"。一段可直接粘进 Claude Code 的**循环章程（charter）**，外加 `/goal`、`/loop` 两个命令的用法。核心一句：**prompting 是亲自做事，loop engineering 是管理那个干活的人。**

- 🔗 出处：[@Raytar — "Stop Being the Loop"](https://x.com/Raytar/status/2069212188619805179)（X 长文，2026-06-23，1.4M 阅读）
- 🔁 配套：和 [`coding/llm-coding-rules-claude-md`](../../coding/llm-coding-rules-claude-md/) 同源思路 —— 那个管"单次写代码的纪律"，这个管"让 Agent 自循环、可中断续跑"。

## 一个循环的五拍

任何循环，再花哨，都是同样五拍：

1. **Find the work** —— 找活：待办、失败的测试、未读邮件、某个文件夹里的文件。
2. **Do it** —— 一次只做一件，像人手工做那样。
3. **Check itself** —— 第二遍自检，确认"做完且正确"，不只是"产出了"。
4. **Remember** —— 写下已完成的，避免重复劳动或丢失进度。
5. **Go again** —— 重复直到没活了，然后停下或叫你。

> 和 cron 定时任务的本质区别：**循环里有个决策者**。cron 跑固定脚本、不思考；循环跑的是 Claude —— 它看当前局面、挑下一步、做、检查结果、再决定继续/重试/撤销/停止。

## 两个命令

```
# /goal —— 有终点线时用：干到"这件事为真"为止，每轮自检是否达标，达标自动停
/goal write a one page brief on [your topic]
where every claim has at least three sources and
every link opens to a real page that supports the claim.

Open each link to confirm it before you call it done.
Replace any source that is dead or does not back up the claim.
Stop only when every source on the page checks out.
```

```
# /loop —— 没有终点、只有节奏时用：按周期反复盯一件事
/loop 30m check whether my live site is back up by loading the homepage.
The moment it returns a normal page, tell me and stop checking.
```

> `30m` = 每 30 分钟。也可直接说 "every morning, triage my inbox"，Claude 会帮你排期。这些是 Claude Code 较新的命令，看不到就升级版本。

## 完整章程 · The Charter（填空即用）

> 小活一行 `/goal` 就够。多步骤大活，给 Claude 一份完整章程：去哪找活、怎么自检、怎么记忆、何时停。填好方括号粘进 Claude Code：

````
You are running as a loop, not answering one prompt. Here is your charter.

GOAL
[Describe the finished state in one or two sentences.
Be specific about what DONE looks like, and make it something you can measure.
Example: "Every product page in /pages has the new pricing and every link opens."]

WHERE THE WORK IS
[Tell Claude where to look.
Examples: "Scan the /pages folder for files with old pricing." Or "Read TODO.md and
treat each unchecked box as a task." Or "Check my connected task board for items tagged ai."]

HOW TO WORK
- Do one item at a time. Finish it fully before starting the next.
- Match the patterns you find in existing files. Do not invent new ones.
- If an item needs a decision only I can make (spending money, deleting things, emailing a
  person), stop on that item, add it to a "needs me" list, and move to the next one.

HOW TO CHECK YOURSELF
After each item, prove it is done before you mark it done.
[Pick what fits: "run the tests" / "re-read the file and confirm it meets the goal" /
"open the link and confirm it loads." Checking means evidence, not confidence.]
If the check fails, fix it and check again. Three tries per item, then log it as blocked and move on.

HOW TO REMEMBER
Keep a file called LOOP-STATE.md.
After each item, write the item name, its status (done / blocked / needs me), what you changed,
and anything the next run should know.
Read this file FIRST every run so you never redo finished work.

WHEN TO STOP
Stop when every item is done or logged as blocked, or when you have finished [N] items this run.
Then give me a short report: what got done, what is blocked, what needs my call.

Start by reading LOOP-STATE.md if it exists, then find the work.
````

## 拆解 · Breakdown

值得复用的编排技巧：

1. **每轮独立自检（generator–verifier 分离）** —— "做完一轮后，第二个 Claude 悄悄检查：到目标了吗？没到就说明原因、继续。" 用**独立验证者**判定 DONE，而不是让生成者自己说"我觉得好了"，是真循环与"跑一次碰运气"的根本区别。
2. **状态文件 = 可中断/可续跑的灵魂** —— 强制 `LOOP-STATE.md`：每件事记下名字/状态/改了啥/下轮须知，且**每轮先读它再干活**。没有它，每次都从零开始；有了它，定时跑也能精确接上次的进度。
3. **证据，而非自信（evidence, not confidence）** —— 自检必须"开链接确认能打开 / 重读文件确认达标 / 跑测试"，明确把"产出"和"验证产出"拆成两步。直击 LLM "自信地编造、不点链接永远以为自己对"的核心失效。
4. **人类决策点显式升级** —— 遇到只有人能拍板的（花钱、删除、发邮件给人），不擅自做，挂到 "needs me" 清单、跳过、继续。把"危险动作"从自动流里隔离出来，是安全自动化的关键护栏。
5. **有界重试 + 明确停止条件** —— "每件事最多三次，仍失败就标 blocked 继续"；停止条件写死（全部完成/被 blocked，或本轮做满 N 件）。避免无限重试烧额度，也避免循环永不收敛。
6. **`/goal`（到终点就停）vs `/loop`（按节奏反复）二分** —— 先按"有没有终点线"选命令，再写章程。把"自动化任务"这个模糊需求，拆成两种可执行形态。
7. **先判断"该不该上循环"** —— 原文三条反例：一次性任务（普通 prompt 更快）、循环更费额度（每件多跑几遍 Claude）、模糊任务不配上循环（"想个更好的产品策略"不是循环，先把真目标定清）。

## 来源 · Source

- 出处：[@Raytar — "Stop Being the Loop. Here's How to Make Claude Work While You Sleep."](https://x.com/Raytar/status/2069212188619805179)（X Article，2026-06-23）。
- 备注：命令与章程原文逐字转录自该长文的可复制代码块；文中引用了 Anthropic 工程师 Boris Cherny "I don't prompt Claude anymore" 的说法。`/goal`、`/loop` 为 Claude Code 内置命令，具体行为以你本地版本为准。
