<div align="center">

[中文](./README.md) · **English**

# 🧰 AI Skills

#### A reusable set of AI skills

[![License](https://img.shields.io/badge/License-MIT-3B82F6?style=for-the-badge)](./LICENSE)
[![Skills](https://img.shields.io/badge/Skills-6-10B981?style=for-the-badge)](#-skills)
[![AgentSkills](https://img.shields.io/badge/AgentSkills-Standard-8B5CF6?style=for-the-badge)](https://agentskills.io)

![Claude Code](https://img.shields.io/badge/Claude_Code-Skill-D97706?style=flat-square&logo=anthropic&logoColor=white)
![Codex](https://img.shields.io/badge/Codex-Skill-10B981?style=flat-square&logo=openai&logoColor=white)
![OpenCode](https://img.shields.io/badge/OpenCode-Skill-3B82F6?style=flat-square)
![OpenClaw](https://img.shields.io/badge/OpenClaw-Skill-8B5CF6?style=flat-square)

</div>

This repository contains reusable AI skills for disk cleanup, AI news lookup, documentation sync, deep research, and long-form Chinese writing.

Every skill here is a structured instruction set that agents load directly. Follows the [Agent Skills](https://agentskills.io) open standard. Works with Claude Code, Codex, OpenCode, and OpenClaw.

---

## 📋 Index

| Name | One-liner | Details |
|---|---|---|
| 💽 [**storage-analyzer**](#-storage-analyzer) | One sentence to scan your whole Mac / Windows drive — three-tier cleanup plan, one-click trash from the browser | [SKILL.md](./storage-analyzer/SKILL.md) |
| 🔥 [**aihot**](#-aihot-ai-hot-news-query) | Lets your agent pull AI HOT's daily report and all AI news from aihot.virxact.com with one Chinese sentence — no API key | [aihot.virxact.com](https://aihot.virxact.com) |
| 🧹 [**neat-freak**](#-neat-freak) | After a session, run `/neat` to reconcile docs, CLAUDE.md, and agent memory, then audit whether project rules are actually followed | [SKILL.md](./neat-freak/SKILL.md) |
| 🔭 [**hv-analysis**](#-hv-analysis-horizontal-vertical-analysis) | Drop a product/company/concept into it and get a 10k–30k word PDF research report | [SKILL.md](./hv-analysis/SKILL.md) |
| ✍️ [**longform-writer**](#-longform-writer) | Makes the agent write long-form Chinese articles with a fixed voice, rhythm, and banned phrase list | [SKILL.md](./longform-writer/SKILL.md) |

---

## 📦 Install

In any agent that supports Skills (Claude Code, Codex, OpenClaw…), just say:

```
Install this skill: https://github.com/forest-USTC/ai-skills/tree/main/<skill-name>
```

Replace `<skill-name>` with the one you want — e.g. `neat-freak`, `hv-analysis`, `longform-writer`. The agent will clone it into the right directory for you.

---

## ✨ Skills

<a id="-skills"></a>

<table>
<tr><td>

### 💽 storage-analyzer

> *"Cleaning Mac junk has been a CleanMyMac job for a decade. Now a single skill replaces it."*

Tell your agent something like "check my storage" or "C: drive is full". It scans your whole disk and opens an **interactive HTML report** in your browser: disk overview, top 5 space hogs, prioritized cleanup, and a 🟢🟡🔴 three-tier list. Every command is one-click-copy; you can also click buttons to move to Trash / delete (always with a second confirmation dialog).

**Why it beats CleanMyMac**

CleanMyMac is a hard-coded program. It'll show you a 3.8 GB Chrome folder labeled "user cache, safe to delete" — but you don't know what's actually inside, which sites you'll log out of, which offline data will be gone.

This skill is agent-driven. Every entry comes with **specific path + content classification + impact of deletion + recommended action**. That mysterious 97 GB UUID Container? It'll tell you it's the Bilibili offline video cache and suggest you clean it through the Bilibili app, not by hand.

**Three-tier classification is the core**

- 🟢 **Green** — Pure caches, temp files. Regenerate automatically. Safe for one-click cleanup
- 🟡 **Yellow** — Contains user data (offline videos, downloads, project code). Only "Open in Finder" and (where safe) "Move to Trash". You decide
- 🔴 **Red** — Running app core data, system files. Explains why not to touch, gives at most "Open folder". Never a delete button

**Hard rules**

Scan phase is **read-only**, period. Deletions require **two clicks** — button on the page, then a browser confirm dialog. The local server runs on 127.0.0.1 + random port + token, with three whitelists (green = can rm; yellow = trash only; both = open).

**🌐 Cross-platform**: macOS fully tested; Windows code-ready (multi-drive supported), worth eyeballing on first run

**How to trigger**

```
check my storage
C drive is full
clean up disk
storage analysis
帮我看看存储
```

→ [SKILL.md](./storage-analyzer/SKILL.md)

</td></tr>
</table>

<table>
<tr><td>

### 🔥 aihot (AI HOT news query)

> *"The AI world ships too much in a day. By the time I notice, it's already old news — let an agent scan it for me."*

Lets any SKILL.md-supporting agent pull AI HOT's daily report and all AI news from [aihot.virxact.com](https://aihot.virxact.com) with one natural Chinese sentence. No API key, no MCP server config.

**What it can do**

- Pull today's or a specific date's AI HOT daily report (pre-packaged by topic)
- Pull the selected items stream (daily editorial candidate pool)
- Pull by category (models / products / industry / papers / tips)
- Pull by time window (last N days)
- Keyword / company / topic search ("recent OpenAI releases", "Sora-related", "RAG papers")

**How to trigger** (Chinese — the underlying API is Chinese-curated)

```
今天 AI 圈有什么新东西
看一下 5 月 6 号的 AI 日报
最近一周的 AI 论文
看下精选条目
最近 OpenAI 有什么发布
```

**🌐 Cross-platform**: Claude Code · Codex CLI · Cursor · Gemini CLI · OpenCode · Cline · Windsurf

**🇨🇳 China-friendly direct install** (no GitHub access needed):

```
curl -fsSL https://aihot.virxact.com/aihot-skill/install.sh | bash
```

→ [SKILL.md](./aihot/SKILL.md) · [aihot.virxact.com](https://aihot.virxact.com) · [Integration guide](https://aihot.virxact.com/agent)

</td></tr>
</table>

<table>
<tr><td>

### 🧹 neat-freak

> *"If I don't run /neat before closing the window, I get itchy. Like there's something stuck in my throat."*

After every session, run `/neat`. It reconciles whatever you changed in this conversation against three layers of project knowledge: **docs**, **root CLAUDE.md / AGENTS.md**, and the **agent's memory system**. It also checks whether project rules are actually being followed, then outputs a change summary at the end.

**Why you'd want this**

You've probably hit this: code has been through 7-8 iterations but the README is still v1.0.0. Memory says you're using SQLite when you actually switched to PostgreSQL months ago. CLAUDE.md lists routes that no longer match the actual server.

The agent isn't getting dumber — your docs and memory are. neat-freak's job is to clean it up.

**It touches three layers**

- Project root CLAUDE.md / AGENTS.md (read by the AI in this project)
- Project docs/ and README (read by teammates and downstream developers)
- The agent's own memory system (read by future you across sessions)

These three layers have different audiences and don't overlap. This version also treats rules as knowledge: CLAUDE.md / AGENTS.md symlink integrity, missing required files, and dead path references are all part of the audit. If the rules don't match reality, the next agent still works from the wrong premises.

**How to trigger**

```
/neat            # direct command
sync up          # natural language
tidy up docs     # natural language
整理一下          # 中文
```

**🌐 Cross-platform**: Claude Code · Codex · OpenCode · OpenClaw

→ [SKILL.md](./neat-freak/SKILL.md)

</td></tr>
</table>

<table>
<tr><td>

### 🔭 hv-analysis (Horizontal-Vertical Analysis)

> *"Vertical axis chases time depth, horizontal axis chases simultaneous breadth. They cross to give you the verdict."*

Want to actually understand what a product / company / concept / person is about? Hand it over.

It runs two threads in parallel: **vertical** — tells the subject's story from inception to the present moment, like a narrative; **horizontal** — lays out every major competitor at the current moment for comparison. When the two cross, you see things that neither current-state nor history alone would show you.

The output is a **typeset PDF research report**, 10,000–30,000 words.

**Good for**

- Competitor research / understanding a new concept / company background research
- Front-loaded research before writing or strategy work
- Wanting to understand a domain from scratch

**Not good for**

- A simple definition lookup — overkill, just ask in regular chat
- Writing a long-form article — that's [longform-writer](#-longform-writer)'s job

→ [SKILL.md](./hv-analysis/SKILL.md)

</td></tr>
</table>

<table>
<tr><td>

### ✍️ longform-writer

> *"A knowledgeable normal person earnestly talking about something that moved them."*

An opinionated writing skill for long-form Chinese public-account articles. Once installed, the agent writes with a fixed voice, rhythm, and banned phrase list.

> ⚠️ **Note for English readers**: This skill produces **Chinese** long-form articles (公众号 / WeChat-style). If your output language is English, this isn't for you. But you might find the methodology interesting as a reference for how to encode a personal voice into a skill.

**Good for**

You want to turn a PDF, transcript, news link, or loose material into a long-form Chinese article with a consistent conversational style.

**Not good for**

You want "good general writing." This skill takes a position. It **refuses** corporate jargon, **refuses** "first... second... finally" structures, **refuses** "in today's rapidly evolving AI landscape" openings. If your target reader actually likes that stuff, this skill isn't for you.

**What's inside**

- Complete style rules (rhythm, narrative, judgment, rhetoric)
- A four-layer self-check system (structure, rhythm, content, language)
- A curated style example library the AI can match against

→ [SKILL.md](./longform-writer/SKILL.md)

</td></tr>
</table>

---

## 🌟 About

These skills can be copied, modified, and redistributed under the license. Read each `SKILL.md` before use to understand triggers, dependencies, and limitations.

---

<div align="center">

[MIT License](./LICENSE) · Free to use, modify, and redistribute

</div>
