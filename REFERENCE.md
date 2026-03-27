# Gary Tools — Reference

Stable facts for this project. Updated in place when facts change.

---

## Quick Reference

| Resource | Value |
|----------|-------|
| Gateway base URL | `https://unified-seo-gateway.kirwan-digital-marketing-ltd.workers.dev` |
| Auth header | `Authorization: Bearer <MCCLATCHY_API_KEY>` |
| Health check | `GET /health` (no auth required) |
| McClatchy brand_id | `mcclatchy` (verify scope — company vs. per-publication) |
| Job polling | `GET /api/v1/jobs/:id` or `?include_output=true` |
| Poll interval | Every 5–10 seconds; stop on `completed` or `failed` |
| Sync timeout | ≥60 seconds for LLM-backed sync endpoints |
| Error capture | Always save `x-request-id` response header for debugging |

---

## Team

| Name | Role | Notes |
|------|------|-------|
| Pierce Williams | Project lead (McClatchy) | Running this repo; next step = follow-up with Chris |
| Chris Palo | McClatchy stakeholder | Driving integration; wants "almost all, maybe all" modules |
| Susannah Locke | Integration lead (McClatchy) | Reviewing Gary's API docs + Jim's materials; scoping timeline |
| Jim Robinson | McClatchy internal SEO | Designed an internal SEO tool; Susannah has that doc; raised novelty concern |
| Stephanie Zandecki | McClatchy internal SEO | Did related internal SEO/content work; also reviewing Gary's toolkit |
| Gary Kirwan | Tool developer | gary@kirwandigital.com — Kirwan Digital Marketing Ltd; will drop API docs + McClatchy key |

---

## What Gary's Toolkit Is

A hosted API (Cloudflare Workers) that takes an article in markdown and runs it through independent audit/improvement modules. McClatchy calls modules à la carte or chains them. Each module is its own API endpoint.

**Key capabilities:**
- **Author persona files** — trains on a writer's existing articles (100K+ words) to produce a voice profile; blends brand guidelines at publication level + individual author level, applied in sequence
- **Modular SEO workflow** — separate agents for research, briefing, SEO title/meta, brand polish, citation checks
- **Deep content validation** — verifies external links are real and relevant; prioritizes Tier 1 sources (journals, encyclopedias, news); finds sources beyond page one to combat hallucinations
- **Internal link builder** — pulls site into a vector database (Convex); suggests internal links by anchor text; prevents orphan pages

Full endpoint reference with request shapes and examples: [docs/api-reference.md](docs/api-reference.md)

---

## Integration Architecture

**Integration point:** Post-CSA generation (CSA produces article → Gary's API audits before editor's desk)

**Recommended full forensic flow:**
1. `POST /audit/citations` — verify claims/links aren't hallucinated
2. `POST /audit/brand-fit` — align to publication voice
3. `POST /polish/brand-fit` — apply findings + insert internal links
4. `GET /audit/internal-links` — suggest additional internal links
5. `POST /optimize/meta` — generate SEO title + meta description
6. `POST /audit/content-structure` — flag heading/skimmability issues

**Deterministic vs. probabilistic principle (Chris's framing):**
- Facts and links = deterministic — human must verify
- Keyword scoring = probabilistic — AI judgment acceptable
- Goal: modular review layer so a content person can confidently sign off on specific elements

**Two-tier brand guidelines (in discussion):**
- `brand-guideline-standard` (national) vs. `brand-guideline-local` (per-publication)
- Relevant for Discover content that syndicates to 4+ sites

---

## High-Value Modules for National Team

| Module | Why it matters | Dependency |
|--------|---------------|------------|
| Citation validation | Addresses hallucination/trust concern; critical for media publisher | None |
| Internal linking | Prevents orphan pages; improves topical depth | McClatchy library must be indexed in Convex first |
| Meta optimization | Post-processing for SEO title/meta even before CSA handles natively | None |
| Brand-fit audit/polish | Aligns to publication voice | McClatchy brand guide must be stored in Gary's system |

---

## Author Voice Roadmap

- **Phase 1 (current):** Content in author's voice based on existing articles
- **Phase 2 (planned):** Loop in which articles performed well → reinforce the voice that *succeeds*, not just their general voice

---

## Related Files

| File | Contents |
|------|----------|
| [docs/api-reference.md](docs/api-reference.md) | Full endpoint map, request shapes, polling patterns, error codes |
| [docs/meeting-notes.md](docs/meeting-notes.md) | Mar 27 kickoff meeting notes |
| [tests/](tests/) | Testing scripts (placeholder — to be populated once API key confirmed) |
| [sessions/2026-03.md](sessions/2026-03.md) | Session archive |
