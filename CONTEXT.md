# Gary Tools — Working Context

**Phase:** Active Evaluation — integration direction confirmed
**Status:** Active — Chris Palo blessed integration (2026-04-01); operational requirements defined; API key pending
**Last session:** 2026-04-01 (Gary reports shared; Chris operational requirements; Pierce tested on Home Buyers Guide)

For stable reference facts: see [REFERENCE.md](REFERENCE.md)
For session history: see [sessions/](sessions/)

---

## Current State

- McClatchy already has a Gary API key; no integration built yet
- Gary shared two claims validation reports (US Weekly legal story; Women's World health article)
- Chris Palo responded: "Love to see how we can integrate this" — formal integration direction confirmed
- Pierce tested Gary's validator on a Home Buyers Guide (Mecklenburg County fiscal year / tax article) with complex real-world nuances that a local editor had flagged
- **Primary use case confirmed:** factual accuracy / claims validation post-CSA, before editor's desk — NOT primarily an SEO play
- Susannah Locke remains integration lead

## Chris Palo's Operational Requirements (2026-04-01)

From email response to Gary's reports:
1. **Editor correction + override:** Editor can correct flagged issues OR override the flag (override should be rare)
2. **Tracking required:**
   - Error rates by article, author, content type
   - Corrections made
   - Override decisions
3. **Override reporting:** Report goes to Sara Vallone + Pierce + Chris initially; shrinks to Sara Vallone (vertical lead) once confident in system
4. **Source trustworthiness management:** Define what counts as trustworthy; McClatchy must be able to remove sources found to be untrustworthy over time

## Open Questions (Must Resolve Before Scoping)

1. Is McClatchy's content library already indexed in Gary's Convex database? (Required for `/audit/internal-links`)
2. Is a McClatchy brand guide stored? (`brand_id: "mcclatchy"`) — Required for brand-fit endpoints
3. What does `brand_id` resolve to — whole company, or per-publication (Miami Herald, KC Star, etc.)?
4. What is the cost model — per API call, per token, or monthly cap?
5. Two-tier brand guidelines: how to handle `brand-guideline-standard` + `brand-guideline-local` for Discover syndication (4+ sites)?

## What's Next — Prioritized

**High:**
1. [ ] Confirm API key receipt and endpoint docs from Gary Kirwan
2. [ ] Build integration spec per Chris's operational requirements (correction/override UX, error tracking, override reporting chain)
3. [ ] Resolve open questions above before scoping begins

**Medium:**
4. [ ] Run first-test sequence once key confirmed: health → scrape → meta → structure → brand-readiness → citations → poll
5. [ ] Check brand readiness: `GET /api/v1/brands/mcclatchy/readiness`
6. [ ] Define source trustworthiness management process (who approves/removes sources)
7. [ ] Add claims validation module to PRD scope (P9) — document as post-CSA quality gate
8. [ ] Explore two-tier brand guideline approach with Chris (local vs. national)
9. [ ] Do NOT wait for SEO team review on non-SEO modules

**Deferred:**
10. [ ] Author voice Phase 2 (loop on high-performing articles) — Gary's roadmap, not yet live
11. [ ] Planned endpoints (SERP analysis, content brief, forum mining) — not yet built

## Session: 2026-04-01 — Chris requirements + Pierce testing

Gary sent two validation reports via email:
- US Weekly legal article — claims validator flagged issues and suggested rewording
- Women's World health article — scientific source checking demonstrated

Chris replied with enthusiasm + operational requirements (see above). Pierce sent Gary a Home Buyers Guide test article (Mecklenburg County tax/fiscal year content with nuanced local issues flagged by an editor) to stress-test the validator.

## Session: 2026-03-31 — Group evaluation commitment

CSA Weekly Update: Chris Palo formally called for evaluation. Group committed to assess each module and return with yes/no. Author portion flagged as most useful; underlying code is MIT open source.

## Session: 2026-03-27 — Context infrastructure setup

Set up three-tier context architecture. Full API reference in `docs/api-reference.md`. Meeting notes in `docs/meeting-notes.md`.

---

*Tiered Context Architecture. Budget: ≤150 lines. Current: ~75 lines.*
