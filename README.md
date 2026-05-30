# KAIZE OS

> the "Kaize OS" that @0x_kaize said he'd open-source but never did. so i built it.

![KAIZE OS](https://img.shields.io/badge/KAIZE%20OS-v1.0-green?style=flat-square)
![Next.js](https://img.shields.io/badge/Next.js-16-black?style=flat-square)
![License](https://img.shields.io/badge/license-MIT-green?style=flat-square)

---

## what is this?

an AI content engine that generates viral X/Twitter posts, threads, hooks, and reply angles.

trained on the exact writing style that got 26M+ impressions. dark terminal UI. real-time viral score analysis. multi-model support (Qwen, Z.AI, OpenAI).

the original creator [@0x_kaize](https://x.com/0x_kaize) promised to open-source this. he hasn't. so here it is — fully functional, no waitlist, no email required.

## features

- **multi-model**: Qwen (DashScope), Z.AI/GLM, OpenAI — auto-detected by model name
- **tone engine**: 4-axis control (casual↔formal, witty, provocative, technical)
- **viral scoring**: LLM-evaluated scores for virality, hook strength, readability, emotional pull
- **format control**: single posts, threads, articles, replies, hook batches
- **platform targeting**: X/Twitter, LinkedIn, long-form
- **quick actions**: rewrite, expand, shorten, formalize, casualize
- **8 templates**: story thread, listicle, POV hook, comparison, rage bait, news breakdown, reply generator, roadmap
- **the exact kaize writing rules** baked into the system prompt — lowercase, punchy, no filler, no "game-changer"/"unlock"/"leverage"

## stack

```
Next.js 16 + TypeScript + Tailwind CSS
OpenAI-compatible API (works with any provider)
Dark terminal aesthetic — JetBrains Mono, green accents
```

## quick start

```bash
# clone
git clone https://github.com/YOUR_USERNAME/kaize-os.git
cd kaize-os

# install
npm install

# configure API keys
cp .env.local.example .env.local
# edit .env.local with your key(s)

# run (requires Node 20+)
nvm use 20  # if using nvm
npm run dev
```

open [http://localhost:3000](http://localhost:3000)

## api configuration

supports any OpenAI-compatible provider. edit `.env.local`:

```bash
# Qwen / DashScope (default)
AI_API_KEY=sk-xxx
AI_BASE_URL=https://dashscope-intl.aliyuncs.com/compatible-mode/v1
AI_MODEL=qwen-latest-series-invite-beta-v34

# Z.AI / ZhiPu / GLM
ZAI_API_KEY=***
ZAI_BASE_URL=https://open.bigmodel.cn/api/paas/v4
```

the app auto-routes to the correct provider based on model name prefix:
- `qwen-*` → DashScope
- `glm-*` → Z.AI
- `gpt-*` → whatever base_url is set

## architecture (what the "tool" actually is)

this is the reverse-engineered architecture of the original Kaize OS:

```
┌─────────────────────────────────────────────┐
│  React Frontend (dark terminal UI)          │
│  ├─ NavSidebar (format selection)           │
│  ├─ ChatPanel (conversation + suggestions)  │
│  └─ WorkspaceSidebar (controls + scores)    │
├─────────────────────────────────────────────┤
│  System Prompt Builder                      │
│  (tone sliders → prompt injection)          │
│  (format/platform → rules concatenation)    │
├─────────────────────────────────────────────┤
│  API Route → OpenAI-compatible LLM          │
│  ├─ Qwen (DashScope)                        │
│  ├─ GLM (Z.AI)                              │
│  └─ GPT-4 (OpenAI)                          │
├─────────────────────────────────────────────┤
│  Score Parser                               │
│  (extracts JSON self-evaluation from LLM)   │
│  (renders animated gauge bars)              │
└─────────────────────────────────────────────┘
```

**the truth**: it's a well-designed UI over an optimized system prompt. the "viral score" is the LLM grading its own homework via structured JSON output. the tone sliders inject adjectives into the prompt. that's it. and that's powerful enough.

## the kaize writing system

the core IP is the writing rules embedded in the system prompt:

- lowercase everything (ALL CAPS for emphasis)
- short sentences. no filler.
- numbers > words ($5k not five thousand)
- lead with the shock
- one idea per line
- em dashes (—) not hyphens
- never say "unlock" "leverage" "delve" "game-changer"
- POV format for viral hooks
- [ BRACKETS ] for structured data

## screenshots

the UI matches the original Kaize OS demo video:
- dark terminal aesthetic
- green accent color scheme
- monospace font (JetBrains Mono)
- right sidebar with model/creativity/tone/scores
- bottom action bar for quick rewrites

## why open source?

the original creator used this as a lead magnet — "download my .md file, wait for the full tool." thousands of people are still waiting.

the .md file IS the tool. the UI is a nice wrapper around it. here's both.

## contributing

PRs welcome. potential additions:
- [ ] conversation persistence (SQLite/localStorage)
- [ ] X API integration for direct posting
- [ ] real-time trending topic injection
- [ ] A/B test mode (generate variants, compare scores)
- [ ] export to markdown/clipboard
- [ ] analytics dashboard (track your post performance)

## license

MIT. do whatever you want with it.

---

*built by reverse-engineering the 26M-impression content system that was promised but never released.*
