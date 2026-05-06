---
title: README — llm-wiki-skill repository
type: summary
created: 2026-05-07
updated: 2026-05-07
sources: [readme]
tags: [llm-wiki, documentation, repository]
---

# README — llm-wiki-skill repository

> Source: `raw/articles/README.md` (project overview).

## One-line takeaway

The **llm-wiki-skill** repo packages a Karpathy-style **compiled Markdown wiki** workflow: agents **ingest** sources into `raw/`, **compile** cross-linked `wiki/` pages, **query** with citations, **lint** graph health, and **audit** human feedback — plus **Obsidian** and **web** tools sharing **`audit-shared`**.

## What the README adds

- **Stack:** `llm-wiki/` (skill + scripts + references), `audit-shared/`, `plugins/obsidian-audit/`, `web/` (Express + client).
- **Install paths:** Cursor skill under `.cursor/skills/llm-wiki/`; Claude/Codex via `~/.claude/skills/` or `~/.codex/skills/`.
- **Ops named explicitly:** `compile`, `ingest`, `query`, `lint`, `audit` — each should append to `log/YYYYMMDD.md`.
- **Related projects:** Karpathy gist, pedronauck/karpathy-kb, Astro-Han/karpathy-llm-wiki, **qmd** for semantic search at scale.

## Links

- Pattern overview: [[LLM Wiki Knowledge Base Pattern]]
- People / tools mentioned: [[Andrej Karpathy]], [[Obsidian]]
