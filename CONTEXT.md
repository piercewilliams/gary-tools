# Gary Tools — Working Context

**Phase:** Evaluation & Integration Scoping
**Status:** Active — group committed to formal evaluation (2026-03-31); awaiting Gary's API key/docs drop
**Last session:** 2026-03-31 (group evaluation commitment made)

For stable reference facts: see [REFERENCE.md](REFERENCE.md)
For session history: see [sessions/](sessions/)

---

## Current State

- McClatchy already has a Gary API key; no integration built yet
- Susannah is integration lead — reviewing Gary's API docs + Jim's materials before scoping timeline
- Gary's toolset is further along than anything internal; Chris wants to integrate directly
- This repo is the learning/experimentation hub for that work

## Open Questions (Must Resolve Before Scoping)

1. Is McClatchy's content library already indexed in Gary's Convex database? (Required for `/audit/internal-links`)
2. Is a McClatchy brand guide stored? (`brand_id: "mcclatchy"`) — Required for brand-fit endpoints
3. What does `brand_id` resolve to — whole company, or per-publication (Miami Herald, KC Star, etc.)?
4. What is the cost model — per API call, per token, or monthly cap?
5. Two-tier brand guidelines: how to handle `brand-guideline-standard` + `brand-guideline-local` for Discover syndication (4+ sites)?

## What's Next — Prioritized

**High:**
1. [x] ~~Follow-up with Chris~~ — Group committed 2026-03-31 to formal evaluation; return with definitive yes/no on integration. Author portion flagged as most useful (underlying code is MIT open source). Political considerations noted.
2. [ ] Gary drops API endpoint docs and McClatchy API key (confirm receipt)
3. [ ] Resolve open questions above before scoping begins
4. [ ] Evaluate each Gary module and return to group with recommendation

## Session: 2026-03-31 — Group evaluation commitment

CSA Weekly Update: Chris Palo formally called for evaluation of Gary's tools. Group (Chris, Sara Vallone, Susannah, Pierce) committed to assess each module and return with definitive yes/no on integration. Author portion flagged as most useful; underlying code is MIT open source. Susannah has had one prior meeting with Gary. Evaluate once API key lands.



**Medium:**
4. [ ] Run recommended first-test sequence once API key confirmed (health → scrape → meta → structure → brand-readiness → citations → poll)
5. [ ] Check brand readiness: `GET /api/v1/brands/mcclatchy/readiness`
6. [ ] Explore two-tier brand guideline approach with Chris (local vs. national for Discover)

**Deferred:**
7. [ ] Author voice Phase 2 (loop on high-performing articles) — Gary's roadmap, not yet live
8. [ ] Planned endpoints (SERP analysis, content brief, forum mining) — not yet built

## Session: 2026-03-27 — Context infrastructure setup

Set up the three-tier context architecture for this repo from scratch. Seeded all three tiers from the Mar 27 kickoff meeting notes and Gary's API documentation shared across two prior conversations.

What was built:
- `CONTEXT.md` — working memory
- `REFERENCE.md` — stable facts (team, architecture, high-value modules, author voice roadmap)
- `sessions/2026-03.md` — session archive
- `docs/api-reference.md` — full Gary API endpoint reference (moved out of REFERENCE.md to keep it lean)
- `docs/meeting-notes.md` — full Mar 27 meeting notes
- `tests/` — placeholder for future test scripts

Team roster fully resolved from transcript: Pierce Williams, Chris Palo, Susannah Locke, Gary Kirwan (gary@kirwandigital.com), Stephanie Zandecki, Jim Robinson. Key addition: Jim Robinson has his own internal SEO tool; Susannah has those materials alongside Gary's docs.

---

*Tiered Context Architecture. Budget: ≤150 lines. Current: ~60 lines.*
