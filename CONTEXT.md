# Gary Tools — Working Context

**Phase:** Active Evaluation — disposition issue, not unresponsiveness
**Status:** Gary has the API endpoint + McClatchy API key ready but will not share location — he prefers to run documents through the tool himself. This is a deliberate choice to maintain control, not a responsiveness issue. Chris Palo told Jason (Smith) about Gary's reluctance (2026-04-07). Sara Vallone following up directly via email (2026-04-08) asking Gary to send endpoint info.
**Last session:** 2026-04-07 (Pierce<>Chris 1:30pm EDT — Gary disposition confirmed; Chris told Jason; Sara following up)

For stable reference facts: see [REFERENCE.md](REFERENCE.md)
For session history: see [sessions/](sessions/)

---

## Current State

- Gary is actively running reports (Duggar legal, Women's World health, Charlotte tax/home values) — API appears live
- **Gary confirmed (2026-04-07):** Has API endpoint + McClatchy API key ready. But will not share location — prefers to run documents through the tool himself. Pierce: "He just wants to run it all himself." Chris confirmed: "Yeah, and for whatever reason he just won't tell us where it is."
- **Chris told Jason (Smith) about Gary's reluctance (2026-04-07):** Chris and Jason went back and forth; Jason now aware Gary is "avoiding" sharing the code.
- Sara Vallone following up via email (2026-04-08): asked Gary directly to send the API endpoint info
- Chris has formally directed Pierce + Sara Vallone to define editorial parameters; Chris reviews once complete
- Four open questions sent to Gary in email chain (2026-04-03); still unanswered
- Home Buyers Guide stress-test complete — Charlotte report strongest of three; caught stale FY2025 tax rate the human editor missed
- CSA fact-checking ruleset v0.1 drafted and passed to Sara Vallone 2026-04-08 — awaiting her review before test article session next week

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
1. [ ] Monitor Sara Vallone follow-up (2026-04-08) — if Gary responds and shares endpoint info, activate testing. If no response, escalate back to Chris.
2. [ ] Sara Vallone parameter session (next week) — walk 15 test articles; v0.1 ruleset already sent to Sara, awaiting her review. Do not wait for Gary's 4 open questions to be answered before running this session.
3. [ ] Gary's 4 questions (confidence scoring, severity calibration, article-level output, reproducibility) — still unanswered; will need to resolve before building integration spec, but don't block Sara session.

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
