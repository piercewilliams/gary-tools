# Gary Tools — Working Context

**Phase:** Active Evaluation — escalated; Chris Palo personally following up
**Status:** Gary still unresponsive to Sara Vallone's test requests (as of 2026-04-06 C&P Weekly). Chris Palo now personally following up; suspects Gary may be deliberately withholding access (prefers team use API → potential future charges on Gary's side). Sara to CC Chris on all further correspondence.
**Last session:** 2026-04-06 (C&P Weekly: Gary unresponsive to Sara's tests; Chris personally following up; escalation escalated)

For stable reference facts: see [REFERENCE.md](REFERENCE.md)
For session history: see [sessions/](sessions/)

---

## Current State

- Gary is actively running reports (Duggar legal, Women's World health, Charlotte tax/home values) — API appears live
- McClatchy API key status unclear: Gary may be running on his end; confirm whether McClatchy's key is active
- Chris has formally directed Pierce + Sara Vallone to define editorial parameters; Chris reviews once complete
- Four open questions sent to Gary in email chain (2026-04-03); awaiting response
- Home Buyers Guide stress-test complete — Charlotte report strongest of three; caught stale FY2025 tax rate the human editor missed
- **Escalation (2026-04-06 C&P Weekly):** Sara Vallone confirmed Gary still unresponsive to her test requests. Chris Palo suspects Gary is hesitant to share tool access — prefers the team go through the API, likely because API usage would generate charges to Gary. Chris committed to personally following up with Gary. Sara to CC Chris on all further correspondence with Gary. Jim Robinson (Engineering) has also flagged a "novelty concern" about Gary's tool — relevance to integration TBD.

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
1. [ ] Await Gary's responses to the four questions (confidence, severity, article-level output, reproducibility) — **Chris Palo now personally following up (2026-04-06)**
2. [ ] Sara Vallone session — approach aligned 2026-04-03: walk reports together, Sara flags what she'd escalate vs. not, Pierce drafts ruleset for iteration. Gated on Gary's answers + Chris's follow-up.
3. [ ] Draft Gary Tools escalation ruleset before Sara Vallone meeting — start from Sara's 2-tier taxonomy (Needs Clarification / Needs Correction); layer in source authority tiers + escalation logic. 15 test articles from Sara.
4. [ ] Confirm API key status — is McClatchy's key active or is Gary running on his end?

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
