# Gary Tools — Working Context

**Phase:** Active Evaluation — API docs received, first-test sequence ready
**Status:** Gary sent full API docs (2026-04-08). Unblocked. New framing from Chris (2026-04-10): Gary's tools are "nodes" — cross-pipeline tools that every pipeline in the CSA system touches. Need to request full roster of all Gary's tools, not just the fact-checking API.
**Last session:** 2026-04-10 — Chris Palo PRD meeting: Gary tools reframed as cross-pipeline nodes; Pierce tasked with contacting Gary for full tool roster.

For stable reference facts: see [REFERENCE.md](REFERENCE.md)
For session history: see [sessions/](sessions/)

---

## Current State

- **UNBLOCKED 2026-04-08:** Gary sent full API documentation ("Unified AI SEO App — Content Audit API (One-Page Report)") to Chris. P10 is now unblocked.
- **Base URL:** `https://unified-seo-gateway.kirwan-digital-marketing-ltd.workers.dev`
- **Auth:** `Authorization: Bearer uak_AWuPNYNP7j2BYi8ZDiAACwPaueknsRHM` — Gary says this key is rotatable ("I can easily rotate the key so this one in the code can be killed for security")
- **Gary's intended workflow:** "Copy this page into your Claude and then run a markdown article through it" — designed to be used via Claude Code, exactly how Pierce works
- Gary is actively running reports (Duggar legal, Women's World health, Charlotte tax/home values) — API confirmed live
- Chris has formally directed Pierce + Sara Vallone to define editorial parameters; Chris reviews once complete
- Four open questions sent to Gary in email chain (2026-04-03); still unanswered
- Home Buyers Guide stress-test complete — Charlotte report strongest of three; caught stale FY2025 tax rate the human editor missed
- CSA fact-checking ruleset v0.1 drafted and passed to Sara Vallone 2026-04-08 — awaiting her review before test article session next week

## API Endpoints (All Live)

| Endpoint | Type | Description |
|----------|------|-------------|
| `GET /health` | sync | Public, no auth — first connectivity test |
| `POST /api/v1/scrape` | sync | URL → markdown |
| `POST /api/v1/optimize/meta` | sync | SEO title + meta description |
| `POST /api/v1/audit/content-structure` | sync | Headings, skimmability |
| `POST /api/v1/audit/unanswered-questions` | sync | Topic gap discovery |
| `POST /api/v1/research/data-validity` | sync or async | **Main fact-checking endpoint.** Requires `keyword`, `goal`, `report_markdown` or `report_path`; infers keyword from headline if not provided |
| `POST /api/v1/audit/citations` | async | Checks linked citations |
| `POST /api/v1/audit/brand-fit` | async | Brand voice comparison |
| `POST /api/v1/polish/brand-fit` | async | Rewrites using brand-fit findings |
| `POST /api/v1/audit/internal-links` | async | Suggests internal links |
| `GET /api/v1/internal-links/library` | sync | Content library for linking |
| `GET /api/v1/brands/:id/readiness` | sync | Check brand readiness |
| `GET /api/v1/brands/resolve` | sync | Resolve publication slug |
| `POST /api/v1/brands/upsert-guide` | sync | Upload brand guide |
| `POST /api/v1/brands/sync-required` | sync | Trigger brand sync |
| `GET /api/v1/jobs/:id` | sync | Poll async job result |

**Async pattern:** POST returns 202 + `job_id` → poll `GET /api/v1/jobs/:id` until complete.
**data-validity pattern:** POST with `wait_for_completion: false` → get `task_id` → poll `GET /api/v1/research/data-validity/:taskId`
**brand_id:** `womans-world-shop` = confirmed working example. `mcclatchy` = referenced in brand-fit examples; readiness not yet confirmed.

## First-Test Sequence

1. `GET /health` — confirm connectivity (no auth needed)
2. `POST /api/v1/scrape` — pull a live article URL → markdown
3. `POST /api/v1/optimize/meta` — SEO title + meta description
4. `POST /api/v1/audit/content-structure` — headings, skimmability
5. `POST /api/v1/audit/unanswered-questions` — topic gaps
6. `GET /api/v1/brands/mcclatchy/readiness` — confirm McClatchy brand is set up
7. `POST /api/v1/audit/citations` (async) — check citations
8. `GET /api/v1/jobs/:id` — poll for async results

## Chris's Directives

- Verdict taxonomy: **TRUE, FALSE, MISLEADING, INSUFFICIENT\_EVIDENCE, OVERGENERALIZED**
- Acceptance tracking = system quality signal (not individual performance); comparable to retraction tracking
- Testing and parameter definition happen in tandem
- "Content call thru and thru" — Pierce owns this with Sara Vallone

## Open Questions (Sent to Gary 2026-04-03)

1. **Confidence score** — what does it actually measure? Not claim accuracy rate (74% confidence / 8 of 9 claims flagged). Likely epistemological — tool's certainty in its own verdicts. Must resolve before parameters can be set.
2. **Severity calibration** — can priority levels be calibrated by content type/domain? All 8 Women's World corrections came back MEDIUM regardless of actual risk.
3. **Article-level vs. claim-level output** — structural/framing issues (MASLD staging omission; Charlotte causal chain) appear in limitations but can't be pinned to claims. Is there a separate output for this?
4. **Reproducibility** — Gary's summary to Chris flagged Redfin data as INSUFFICIENT\_EVIDENCE; full report marked it TRUE. Were these different runs? Task status on Charlotte report was "stopped," not "completed."

## What Pierce Needs to Do with Sara Vallone

**Goal:** Define the editorial parameters McClatchy National is comfortable with. Bring to Chris for review.

**Specific decisions to make together:**
1. Which verdict types require editor action before publish? (FALSE = yes; MISLEADING = probably yes; OVERGENERALIZED / INSUFFICIENT\_EVIDENCE = judgment call)
2. Does severity threshold vary by content type? (legal, health, local government all demonstrated different profiles)
3. What does acceptance tracking look like operationally? (per claim, per article, per content type, per author)
4. What's the reporting cadence and audience? (Chris said: Sara + Pierce + Chris initially, then shrinks to Sara)

**How to run the meeting:** Use the three reports as working examples — walk each one and ask "would we require the reporter to address this?" That produces parameters organically rather than abstractly. Arrive with a draft threshold recommendation Sara can react to; don't run it as a Q&A.

## What's Next — Prioritized

**High:**
1. [ ] **Contact Gary Kirwan for full roster of all tools he has built** — copy Chris Palo on the email. Gary likely has tools beyond the fact-checking/content audit API documented here. Chris wants to understand which tools function as "nodes" across all pipelines.
2. [ ] **Run first-test sequence** (see table above) — health → scrape → meta → content-structure → unanswered-questions → brands/mcclatchy/readiness → citations → poll. Use McClatchy key in hand.
3. [ ] **Sara Vallone parameter session (next week)** — walk 15 test articles; v0.1 ruleset already sent to Sara 2026-04-08, awaiting her review. Do not wait for Gary's 4 open questions to be answered before running this session.
3. [ ] Gary's 4 questions (confidence scoring, severity calibration, article-level output, reproducibility) — still unanswered; will need to resolve before building integration spec, but don't block Sara session or first-test sequence.

**Medium:**
4. [ ] Draft parameters document for Chris review once Sara session complete
5. [ ] Run first-test sequence with McClatchy key once confirmed: health → scrape → meta → structure → brand-readiness → citations → poll
6. [ ] Define source trustworthiness management process (Pierce owns list per Chris)
7. [ ] Add claims validation module to PRD scope (P9)

**Deferred:**
8. [ ] Resolve open questions (Convex indexing, brand_id scope, cost model, author voice endpoint) — still pending Gary's API docs
9. [ ] Two-tier brand guideline approach — Chris proposed; not yet scoped
10. [ ] Author voice Phase 2 — Gary's roadmap, not yet live

---

*Tiered Context Architecture. Budget: ≤150 lines. Current: ~100 lines.*
