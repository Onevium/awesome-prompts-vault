# Awesome Prompts Vault

> A curated vault of **prompts** — system prompts, coding prompts, agent/tool-orchestration prompts, and original creations — organized for study and reuse, not just copy-paste.

[![License: CC BY 4.0](https://img.shields.io/badge/License-CC%20BY%204.0-lightgrey.svg)](./LICENSE)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](./CONTRIBUTING.md)
[![Prompts](https://img.shields.io/badge/prompts-1-orange.svg)](#catalog)

[简体中文](./README.md) · **English**

---

## Why a vault, not a list

Most prompt repos are walls of text you skim once. This one treats each prompt as a **studied artifact**: **every prompt is its own folder** with a `README.md` (intro + usage + breakdown + sources) that extracts the *reusable techniques* — layered structure, hard-constraint-first phrasing, explicit capability boundaries — so you learn the craft, not just the copy.

```
prompts/<category>/<slug>/
├── README.md          # intro + usage + breakdown + sources (with frontmatter)
└── <slug>.txt         # optional: raw original if > 5000 chars
```

## Catalog

| Category | What lives here | Count |
| --- | --- | --- |
| [`system-prompts/`](./prompts/system-prompts/) | Full system prompts, by source (anthropic / openai / google / community) | **1** |
| [`coding/`](./prompts/coding/) | Code generation, review, refactor | _0_ |
| [`agent/`](./prompts/agent/) | Agent loops, tool definitions, multi-agent orchestration | _0_ |
| [`creative/`](./prompts/creative/) | Writing, design, ideation | _0_ |
| [`mine/`](./prompts/mine/) | Original and remixed prompts | _0_ |

### 🔥 Featured

- **[Claude Fable 5 system prompt (extracted)](./prompts/system-prompts/anthropic/claude-fable-5/)** — debunking the "cracked version" myth + the full 122,750-char original + a structural breakdown.

## Anatomy of an entry

Every prompt is a Markdown note. Start from [`templates/PROMPT.template.md`](./templates/PROMPT.template.md):

```yaml
---
name: ...
prompt_type: system-prompt | coding | agent | creative
source_org: anthropic | openai | google | community | mine
use_case: [agent, design, ...]
model: ...
status: captured | refined | original
source_variant: leaked        # only for extracted/leaked prompts
---
```

The **`## Breakdown`** section is the soul of every note — at least 3–5 reusable techniques, not a restatement of what the prompt says.

## A note on extracted prompts

Some entries are *extracted* or *leaked* system prompts published by third parties. They're included for **research** — studying safety design, tool definitions, and prompt structure. They are not jailbreaks and don't unlock anything. Extracted entries are tagged `source_variant: leaked` and credited to their source. If you own content here and want it removed, open an issue.

## Contributing

See [CONTRIBUTING.md](./CONTRIBUTING.md). One prompt per note, real frontmatter, and a Breakdown that teaches something.

## Acknowledgments

Inspired by the broader prompt-engineering and system-prompt-research community that documents how frontier models are steered. Sources are credited per entry.

## Built & maintained by

Curated and maintained by **[Onevium](https://github.com/Onevium/Onevium)** — a personal AI superapp powered by Claude Code: automate the browser, schedule the work, deploy bots, all from one desktop. If this vault helps, drop by [Onevium](https://onevium.com) and leave a ⭐.

## Star History

[![Star History Chart](https://api.star-history.com/svg?repos=Onevium/awesome-prompts-vault&type=Date)](https://star-history.com/#Onevium/awesome-prompts-vault&Date)

## License

Content licensed [CC BY 4.0](./LICENSE) © 2026 onevium.dev — reuse freely with attribution.
