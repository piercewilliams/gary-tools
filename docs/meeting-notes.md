# Meeting Notes

---

## 2026-03-27 — CSA / Gary Tools Kickoff

**Attendees:** Gary Kirwan, Chris Palo, Susannah Locke, Pierce Williams, Stephanie Zandecki, Jim Robinson

**Purpose:** Chris Palo convened to bring together internal (Stephanie, Jim) and external (Gary) SEO/content AI work and determine how it integrates into the Content Standardization Agent (CSA) workflow.

### Key Points

**Author persona & voice integration**
Gary trained a model on Sara Vallone's articles (100K+ words) to produce an "author profile" that personifies content in her voice. Testing included running content through AI probability tools to increase human-likeness scoring. Long-term vision: an agentic layer that, if content is assigned to an author, produces it in their voice.
- Phase 1: content in author's voice
- Phase 2: loop in which articles performed well → reinforce the voice that *succeeds*, not just their general voice

**Modular SEO workflow**
Modules built in Cloudflare, available via single API calls. McClatchy dev team can call specific modules à la carte.

**Content validation & linking**
Link verification and claim validation identified as crucial. Internal link builder consults a vector database (Convex) to suggest internal links by anchor text. Validation checker prioritizes Tier 1 sources (journals, encyclopedias, news) to combat hallucinations.

**Deterministic vs. probabilistic (Chris)**
Facts and links must be deterministic — a human must be able to verify them. Keyword scoring can be probabilistic. Goal: modular review layer so a content person can confidently sign off on specific elements without editing the whole article.

**Two-tier brand guidelines (Chris)**
Wants `brand-guideline-standard` + `brand-guideline-local` vs. `brand-guideline-national` — relevant for Discover content that syndicates to 4+ sites with different local/national flavor.

**Novelty concern (Jim)**
Is this just aggregating existing information? Gary's answer: deep claim checks + information foraging + structured formatting (HTML tables, bullets) add value beyond page-one consensus.

**Internal tools**
Jim Robinson designed a related internal SEO tool. Susannah Locke has those materials and is also reviewing Gary's API docs before scoping the integration timeline.

### Closing

Chris acknowledged Gary's toolset is further along than anything internal and wants to integrate it directly — "almost all of them, maybe all of them." Stephanie and Jim were seeing this material for the first time; Susannah offered time to digest before follow-up.

Chris explicitly noted: "There are elements of this that don't have anything to do with SEO to be frank. SEO is probably one of 10 things" in Gary's toolkit.

### Action Items

- Chris to talk with Pierce about which modules to integrate
- Gary to drop API endpoint docs and McClatchy API key
- Susannah to scope timeline after reviewing Gary's docs + Jim's materials
- Stephanie and Jim to review and identify where they see value
