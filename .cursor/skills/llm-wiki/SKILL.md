---
name: llm-wiki
description: >-
  Builds and maintains a Karpathy-style LLM knowledge base — a self-compiling
  Obsidian Markdown wiki where the Cursor agent ingests raw sources, compiles
  cross-linked concept/entity/summary pages, answers queries against the corpus,
  lints the graph for health, and processes human feedback filed from Obsidian
  or the local web viewer. Use when (1) scaffolding a new knowledge base,
  (2) ingesting articles/papers/PDFs into raw/, (3) compiling or restructuring
  wiki articles, (4) answering questions against the wiki and filing durable
  answers, (5) running lint for dead links, orphans, coverage gaps, audit shape,
  (6) processing feedback from audit/. Not for general note-taking or
  non-wiki Obsidian use. Requires a wiki root (often created with
  llm-wiki/scripts/scaffold.py from this repository).
---

# LLM Wiki — Karpathy knowledge base (Cursor)

> **Experimental — iterating.**  
> Inspired by [Karpathy's llm-wiki Gist](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f).

## Cursor setup

- This skill lives at **`.cursor/skills/llm-wiki/`** in this repository (project skill). Copy that folder into another repo’s **`.cursor/skills/llm-wiki/`** if you want the same workflow there.
- Enable the skill when working on a wiki (Rules / Agent skills / `@llm-wiki`, depending on your Cursor version).
- **Repository layout:** companion scripts and reference docs are under **`llm-wiki/`** at the workspace root. Commands below assume the workspace is the **`llm-wiki-skill`** repo (or a fork) so paths like `llm-wiki/scripts/scaffold.py` resolve.

## Core idea

Instead of RAG (re-fetching raw docs every query), the agent **compiles** sources into a persistent, cross-linked wiki. Every ingest, query, lint, and audit pass makes the wiki richer.

- **You:** source material, questions, direction, structured feedback when the wiki is wrong.
- **Cursor agent:** writing, cross-linking, filing, bookkeeping, applying feedback.

Five operations: **`compile`**, **`ingest`**, **`query`**, **`lint`**, **`audit`**. At session start, read **`CLAUDE.md`** and **`wiki/index.md`** in the wiki root.

### About the filename `CLAUDE.md`

The wiki schema file is still named **`CLAUDE.md`** (Karpathy / ecosystem convention). It is **not** Claude-specific: it is the single schema for scope, naming, article inventory, and gaps. The Cursor agent treats it like a project constitution for the wiki. Deeper field-by-field help: `llm-wiki/references/schema-guide.md`.

## Directory layout

```
<wiki-root>/
├── CLAUDE.md          ← Schema: scope, conventions, articles, gaps
├── log/
├── audit/
│   └── resolved/
├── raw/
│   ├── articles/
│   ├── papers/
│   ├── notes/
│   └── refs/
├── wiki/
│   ├── index.md
│   ├── concepts/
│   ├── entities/
│   └── summaries/
└── outputs/
    └── queries/
```

## Core principles

### 1. Divide and conquer

Target **400–1200 words** per page. If a topic exceeds that: `wiki/concepts/<topic>/` with `index.md` + aspect files; reflect hierarchy in `wiki/index.md`.

### 2. Mermaid and KaTeX

Diagrams → **mermaid** only (no ASCII flow art). Math → **KaTeX** (`$...$` or `$$...$$`).

### 3. Raw file policy

Small text sources → `raw/<subfolder>/`. Large binaries → pointer files under `raw/refs/<slug>.md` with `kind: ref` and `external_path` (see main references).

### 4. Audit channel

Humans file feedback via Obsidian plugin or web viewer → one YAML-frontmatter file per item in `audit/`. The agent **must** run the **`audit`** operation periodically; applied feedback moves to `audit/resolved/` with a `# Resolution` section and a `log/` entry.

---

## The five operations

Each operation appends a line to **`log/YYYYMMDD.md`** (`## [HH:MM] <op> | ...`).

### 1. `compile`

Restructure wiki from existing `raw/` (splits, merges, `index.md` rebuild).

**Steps:** Read `CLAUDE.md`, `wiki/index.md`, target subtree. Split oversized pages (confirm with user). Merge near-duplicates (confirm). Regenerate `index.md`. Log.

### 2. `ingest`

**Steps:** Save source under `raw/…`. Read fully. Add `wiki/summaries/<slug>.md`. Update concepts/entities. Update `wiki/index.md`. Log.

### 3. `query`

Answer from the **wiki**, not generic web knowledge.

**Steps:** Use `wiki/index.md`; read linked pages; if insufficient, say so and suggest ingest targets. Save answer under `outputs/queries/…`. Promote durable synthesis to `wiki/concepts/` when appropriate. Log.

### 4. `lint`

From the **repository root** (this workspace):

```bash
python llm-wiki/scripts/lint_wiki.py <wiki-root>
```

(On Unix you may use `python3` instead of `python`.) Fix issues with user confirmation; log.

### 5. `audit`

```bash
python llm-wiki/scripts/audit_review.py <wiki-root> --open
```

Resolve each open audit (accept / partial / reject / defer), append `# Resolution`, move to `audit/resolved/`, log. Never delete audit files.

---

## Tooling (paths relative to this repo root)

| Piece | Path |
|-------|------|
| Scaffold | `llm-wiki/scripts/scaffold.py` |
| Lint | `llm-wiki/scripts/lint_wiki.py` |
| Audit review | `llm-wiki/scripts/audit_review.py` |
| Obsidian plugin | `plugins/obsidian-audit/` |
| Web viewer | `web/` |

Build web + plugin per `README.md`. The plugin and web stack share **`audit-shared/`** so audit files match.

## Starting a new wiki

From the **repository root**:

```bash
python llm-wiki/scripts/scaffold.py <wiki-root> "<Topic Title>"
```

Then fill `CLAUDE.md`, ingest, query, lint, and process audits as above.

## `wiki/index.md` and `log/`

- **Index:** Every page exactly once; hierarchical bullets for folder-split concepts. See body examples in the original pattern; `lint` enforces coverage.
- **Log:** One file per day; ops tagged `compile`, `ingest`, `query`, `lint`, `audit`, `promote`, `split`, `scaffold`. Details: `llm-wiki/references/log-guide.md`.

## Use cases

Research wikis, personal encyclopedias, team KBs fed by notes, reading companions.

## References (read from workspace `llm-wiki/` tree)

- `llm-wiki/references/schema-guide.md` — `CLAUDE.md` contents
- `llm-wiki/references/article-guide.md` — article style, links, mermaid, math
- `llm-wiki/references/log-guide.md` — `log/` convention
- `llm-wiki/references/audit-guide.md` — audit format and workflow
- `llm-wiki/references/tooling-tips.md` — Obsidian, web viewer, qmd, plugin

## Windows notes

- Prefer **`python`** and **UTF-8** console (`chcp 65001` or `PYTHONIOENCODING=utf-8`) if scaffold/lint print Unicode checkmarks.
- **`npm start`** for `web/`: run inside **`web/`**; on PowerShell, if flags are dropped, use  
  `npx tsx server/index.ts --wiki "<wiki-root>" --port 4175`  
  or `npm start -- --wiki="<wiki-root>" --port=4175`.
