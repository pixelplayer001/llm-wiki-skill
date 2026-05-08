# Client portal and hybrid chain explanation
_Exported on 5/8/2026 at 23:49:24 GMT+8 from Cursor (3.3.27)_

---

**User**

explain client portal and hybrid chain

---

**Cursor**

Gathering project documentation and code references for "client portal" and "hybrid chain".



Here is a concise picture from how Forty-Two documents it.

## Client portal (PathLLM.ai)

In this repo, the **client portal** is modeled as external surfaces under `components/external-component/client-portal/`. The piece that matters for synthesis is **`ClientPortalSynthesis`**: a **wizard** where users set **request scope**, **structure**, **output settings**, then use **“Submit Batch”** to kick off backend synthesis chains.

```1:19:c:\projects\pathllm\letsmod\forty-two\components\external-component\client-portal\client-portal-synthesis.json
{
  "term": "ClientPortalSynthesis",
  "category": "external-component",
  "definition": "[ClientPortalSynthesis] is the external client portal wizard where users define request scope, structure, output settings, and submit synthesis batches.",
  "relationships": {
    "references": [
      "[SynthesisBatch]",
      "[Request]",
      "[Policy]",
      "[Storyboard]",
      "[Storyline]"
    ],
    "triggers": [
      "[VideoSynthesizer]",
      "[HybridVideoCreatorSynthesizer]",
      "[StorySynthesizer]",
      "[SegmentRemixSynthesizer]"
    ]
  },
```

Routing by **structure mode** (standard vs storyboard vs story-only vs remix) is a **business rule** on that component; the exact API condition that picks one chain over another is still called out as something to canonicalize (see `known-gaps` in the same file).

---

## Hybrid chain (`HybridVideoCreatorSynthesizer`)

**“Hybrid”** here means the pipeline that **mixes client-portal inputs with mined / video-analysis content** and then **generates scenes** where needed.

**`HybridVideoCreatorSynthesizer`** is a **top-level chain** with two sub-chains in order:

1. **`HybridVideoCreator`** — load an existing **`Video`** (+ scope, request, optional **storyboard**), assign **pattern** (storyboard-driven vs autonomous), **assemble** the video token (verbs, segments, hybrid assembly).
2. **`VideoSceneCreator`** — **scene video generation** (e.g. Veo, optional Runway base shots) for content that is not satisfied from existing material.

```1:25:c:\projects\pathllm\letsmod\forty-two\chains\hybrid-video-creator-synthesizer\hybrid-video-creator-synthesizer-chain-component.json
{
  "$schema": "../../core-schemas/chain-component-schema.json",
  "term": "HybridVideoCreatorSynthesizer",
  "category": "chain",
  "definition": "[HybridVideoCreatorSynthesizer] orchestrates hybrid video creation and scene synthesis. [HybridVideoCreator] handles the full creation pipeline — resolving input data, then creating hybrid videos in dual mode (storyboard-driven or autonomous) with equal source evaluation from a unified candidate pool and hybrid assembly combining client-portal and video-analysis content. Then [VideoSceneCreator] generates scene videos for tokens that were created from scratch (not sourced from existing content), using Gemini Veo for scene generation and optional Runway video-to-video for base-shot videos.",
  "portalTrigger": {
    "portalComponent": "[ClientPortalSynthesis]",
    "page": "Synthesis",
    "cta": "Submit Batch",
    "routingCondition": "storyboard enabled with per-segment constraints",
    "lifecycle": "active",
    "sourceIdea": "workspace/ideas/2026-04-01-008-hybrid-video-creator-synthesizer-portal-map.md"
  },
  "members": [
    {
      "type": "chain",
      "name": "HybridVideoCreator",
      "order": 1
    },
    {
      "type": "chain",
      "name": "VideoSceneCreator",
      "order": 2
    }
  ]
}
```

**Portal link:** the chain definition’s `portalTrigger` says this path is the **Synthesis** tab, **Submit Batch**, when **storyboard is on with per-segment constraints** (the idea doc frames that as the portal’s most granular storyboard-driven flow). **`VideoSynthesizer`** is documented as the more **standard** path when storyboard is off or not driving per-segment locks.

**Runtime note:** the hybrid synthesizer expects a **Video already in the DB** before `VideoInputResolver` runs; the skill doc spells out scope/segment/storyboard prerequisites for NEO runs.

---

**One-line distinction:** the **client portal** is the **UI + contracts** that submit work; **`HybridVideoCreatorSynthesizer`** is the **backend chain** that implements **storyboard-heavy hybrid assembly + scene generation**, as opposed to the standard **`VideoSynthesizer`** path or story-only **`StorySynthesizer`**.

---

**User**

Is there a usage guide for Client Portal and Hybrid Chain

---

**Cursor**

Searching the repo for Client Portal and Hybrid chain documentation.



Here is what exists in **this** repo (Forty-Two):

## Client Portal — no dedicated usage guide

There is **not** a step-by-step “how to use the Client Portal” document. What you do have:

- **External surface definitions** (concepts, CTAs, triggers): `components/external-component/client-portal/*.json` (e.g. `client-portal-synthesis.json` for the synthesis wizard).
- **Short glossary entries**: `docs/context/glossary.md` (`ClientPortalSynthesis`, `ClientPortalUpload`, `ClientPortalVideos`, etc.).
- **Engineering “portal map” notes** (ideas, not end-user docs): `workspace/ideas/2026-04-01-006-video-synthesizer-portal-map.md`, `workspace/ideas/2026-04-01-008-hybrid-video-creator-synthesizer-portal-map.md`, and similar `*-portal-map.md` files.

Several of those ideas point at a **master** doc, `docs/ideas/2026-04-01-001-client-portal-pipeline-map.md`, but that file **is not in the repository** (some idea files explicitly say the master map is missing and the per-chain portal maps are the in-repo stand-in). Actual **PathLLM.ai UI** behavior and user-facing help would live in whatever repo hosts the portal, not in Forty-Two.

---

## Hybrid chain — yes, an operational guide (for running it)

The closest thing to a **usage guide** for **HybridVideoCreatorSynthesizer** is:

**`.claude/skills/run-hybrid-video-creator-synthesizer/SKILL.md`**

It covers what the chain does, prerequisites (pre-existing `Video`, scope, segment-images, storyboard modes), **running via NEO** (auth, service name from the Services Registry spreadsheet, `videoId`), monitoring, verification, and troubleshooting.

The **chain definition** (including portal trigger text) is in `chains/hybrid-video-creator-synthesizer/hybrid-video-creator-synthesizer-chain-component.json`.

---

**Summary:** Forty-Two documents the **platform contracts** and **how to run/debug the hybrid chain** (especially via NEO); it does **not** ship a Client Portal end-user manual. If you need a true “how to click through the portal” guide, that is likely another codebase or internal wiki outside this repo.

