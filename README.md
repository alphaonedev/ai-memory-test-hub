# ai-memory-test-hub

**Quality-gates hub for ai-memory releases.** Aggregates the existing test-gate
repos and presents per-release testing evidence on GitHub Pages.

> Live hub: <https://alphaonedev.github.io/ai-memory-test-hub/>

---

## What this repo is

A **single entry point** for everyone who asks "is this ai-memory release tested?"
Instead of pointing them at three different repos and asking them to correlate,
this hub presents:

- **Per-release evidence pages** — one folder per release tag with the gate-by-gate
  results, links to the underlying run artifacts, and a single-line verdict.
- **Aggregated dashboard** — current state across all gates for the latest release
  (and the in-flight one).
- **Cross-references** — every release page deep-links to the matching runs in
  `ai-memory-ship-gate` and `ai-memory-ai2ai-gate`.

This repo does **not** run tests itself. It's a presentation layer over the
gate repos that already do the work.

## The gate repos

| Repo | Purpose | URL |
|---|---|---|
| `ai-memory-ship-gate` | Release testing — Phase 1 functional, Phase 2 multi-agent, Phase 3 migration, Phase 4 chaos | <https://github.com/alphaonedev/ai-memory-ship-gate> · [pages](https://alphaonedev.github.io/ai-memory-ship-gate/) |
| `ai-memory-ai2ai-gate` | **Umbrella spec** — testbook, scenario contracts, v1-GA criteria. The umbrella holds the spec; per-release execution lives in `ai-memory-a2a-v<version>` repos. | <https://github.com/alphaonedev/ai-memory-ai2ai-gate> · [pages](https://alphaonedev.github.io/ai-memory-ai2ai-gate/) |
| `ai-memory-a2a-v0.6.3.1` | **Per-release execution (in flight)** — A2A campaign on a 4-node DigitalOcean mesh against `ai-memory v0.6.3.1` (tag pinned 2026-04-30). 24 scenarios (S1–S24); S9–S22 are v0.6.3.1-specific surfaces. Findings funnel into Patch 2 (#511). | <https://github.com/alphaonedev/ai-memory-a2a-v0.6.3.1> · [pages](https://alphaonedev.github.io/ai-memory-a2a-v0.6.3.1/) |
| `ai-memory-test-hub` (this repo) | Aggregator + per-release evidence presentation | <https://github.com/alphaonedev/ai-memory-test-hub> · [pages](https://alphaonedev.github.io/ai-memory-test-hub/) |

## Layout

```
docs/                        # GitHub Pages root
  index.html                 # hub landing page
  releases/
    v0.6.3/
      index.html             # v0.6.3 evidence page
      ship-gate.html         # ship-gate phase results
      a2a-gate.html          # a2a-gate certification matrix
      summary.json           # machine-readable verdict
    v0.6.2/
      ...
analysis/                    # ad-hoc analysis notebooks (git-only, not Pages)
campaigns/                   # per-release test campaign briefs
  v0.6.3-phase2.md           # what gets tested for v0.6.3, in what order
```

## Adding evidence for a new release

1. Create `docs/releases/v<version>/index.html` from the template at
   `docs/releases/_template/`.
2. Run ship-gate phases 1-4 against the release branch. Capture artifacts
   in `ai-memory-ship-gate` per its existing process.
3. Run a2a-gate certification cells against the release tag. Capture
   in `ai-memory-ai2ai-gate` per its existing process.
4. Embed/link the run URLs from those repos into the evidence page here.
5. Commit + push. GitHub Pages auto-builds.

## License

Apache 2.0 — same as ai-memory itself.

---

*Hub created 2026-04-27 to centralize testing evidence for the v0.6.3 release
campaign and onward. v0.6.3 shipped 2026-04-27. v0.6.3.1 shipped 2026-04-30
with a per-release a2a campaign in flight at
<https://alphaonedev.github.io/ai-memory-a2a-v0.6.3.1/>. Older v0.6.x
evidence will be backfilled as time permits.*
