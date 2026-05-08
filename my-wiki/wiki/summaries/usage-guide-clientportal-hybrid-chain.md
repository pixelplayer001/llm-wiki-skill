---
title: PathLLM — Client Portal vs hybrid chain (usage docs inventory)
type: summary
created: 2026-05-09
updated: 2026-05-09
sources: [usage-guide-clientportal-hybrid-chain]
tags: [pathllm, forty-two, client-portal, hybrid-video, synthesis]
---

# PathLLM — Client Portal vs hybrid chain (usage docs inventory)

> Source: `raw/articles/pathllm/usage_guide_for_clientportal_and_hybrid_chain.md` (Cursor export, 2026-05-08).

## One-line takeaway

In the **Forty-Two** (PathLLM.ai) codebase, **Client Portal** is the **external synthesis wizard** (`ClientPortalSynthesis`); **hybrid chain** is the backend **`HybridVideoCreatorSynthesizer`** pipeline. The repo documents **contracts and operators**, not an end-user portal click-through guide.

## What exists in-repo

| Topic | Usage guide? | Where to look |
|--------|----------------|---------------|
| **Client Portal** | No dedicated step-by-step | JSON under `components/external-component/client-portal/`, `docs/context/glossary.md`, `workspace/ideas/*-portal-map.md`; master `docs/ideas/2026-04-01-001-client-portal-pipeline-map.md` cited as **missing** |
| **Hybrid chain** | Yes — operational | `.claude/skills/run-hybrid-video-creator-synthesizer/SKILL.md` (NEO runs, prerequisites, troubleshooting); chain JSON in `chains/hybrid-video-creator-synthesizer/` |

## Distinction (product sense)

- **Client portal:** UI + **Submit Batch** flows that enqueue work; structure modes (standard / storyboard / story-only / remix) drive **which synthesizer** runs.
- **Hybrid chain:** **HybridVideoCreator** (assemble from client inputs + mined/video-analysis) then **VideoSceneCreator** (scene gen for tokens not covered by existing media); portal trigger aligns with **storyboard + per-segment constraints** vs **`VideoSynthesizer`** for simpler paths.

## Links

- Compiled concept: [[PathLLM Client Portal and Hybrid Video Chain]]
- Platform entity: [[Forty-Two]]
