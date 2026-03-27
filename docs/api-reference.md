# Gary Tools — API Reference

Source: Gary Kirwan (gary@kirwandigital.com) / Kirwan Digital Marketing Ltd
Gateway: Cloudflare Workers — do not call the origin/container directly.

---

## Base URL & Auth

```
Base URL:  https://unified-seo-gateway.kirwan-digital-marketing-ltd.workers.dev
Auth:      Authorization: Bearer <MCCLATCHY_API_KEY>
```

`/health` is public (no auth). All `/api/*` routes require the bearer token.

Capture the `x-request-id` response header on any failed request — required for debugging with Gary.

---

## Sync Endpoints

Return results immediately.

| Endpoint | Method | Purpose |
|----------|--------|---------|
| `/health` | GET | Gateway liveness check (no auth) |
| `/api/v1/optimize/meta` | POST | SEO title + meta description |
| `/api/v1/audit/content-structure` | POST | Headings, skimmability, paragraph length |
| `/api/v1/scrape` | POST | Convert a URL to markdown |
| `/api/v1/research/data-validity` | POST | Deep research claim validation |
| `/api/v1/research/data-validity/:taskId` | GET | Poll research task |
| `/api/v1/internal-links/library` | GET | View indexed content library |
| `/api/v1/brands/:id/readiness` | GET | Check brand guide + library readiness |
| `/api/v1/brands/resolve` | GET | Resolve brand by publication |
| `/api/v1/brands/upsert-guide` | POST | Upload/update brand guide |
| `/api/v1/brands/sync-required` | POST | Check if library sync is needed |

Sync LLM-backed endpoints (meta, content-structure): use ≥60s timeout.

---

## Async Endpoints

Return `{ "job_id": "...", "status": "queued" }` immediately. Poll `/api/v1/jobs/:id`.

| Endpoint | Method | Purpose |
|----------|--------|---------|
| `/api/v1/audit/citations` | POST | Verify claims; check link validity |
| `/api/v1/audit/brand-fit` | POST | Score content against brand voice |
| `/api/v1/polish/brand-fit` | POST | Rewrite applying brand-fit findings |
| `/api/v1/audit/internal-links` | POST | Suggest internal links from content library |

**Polling:**
```
GET /api/v1/jobs/:id
GET /api/v1/jobs/:id?include_output=true   # include result payload
```
Poll every 5–10 seconds. Stop on `completed` or `failed`. Polling timeout: 15–30s is fine.

---

## Content Input Rules

Most endpoints accept either:
- `markdown` — raw article string
- `url` — public page to scrape first

Additional required fields by endpoint:
- `brand_id` — required for brand-fit and internal-link endpoints
- `findings` — required for `/polish/brand-fit` (from a prior brand-fit audit)
- `target_keyword` — optional on meta and structure audits

---

## Key Endpoint Details

### POST /api/v1/optimize/meta
```json
{
  "markdown": "...",
  "target_keyword": "hurricane insurance costs",
  "mode": "basic"    // "basic" | "enhanced" | "both"
}
```

### POST /api/v1/audit/content-structure
```json
{
  "markdown": "...",
  "target_keyword": "flood insurance explained",
  "format": "report"   // optional — returns Markdown instead of JSON
}
```

### POST /api/v1/audit/citations
```json
{
  "markdown": "..."
}
```
Returns 202 + job_id. Poll for result.

### POST /api/v1/audit/brand-fit
```json
{
  "brand_id": "mcclatchy",
  "markdown": "..."
}
```
Returns 202 + job_id.

### POST /api/v1/polish/brand-fit
```json
{
  "brand_id": "mcclatchy",
  "markdown": "...",
  "findings": [{ "issue": "...", "recommendation": "..." }],
  "include_internal_links": true,
  "auto_insert_internal_links": false,
  "append_product_section": false
}
```
Returns 202 + job_id.

### POST /api/v1/audit/internal-links
```json
{
  "brand_id": "mcclatchy",
  "markdown": "..."
}
```
Returns 202 + job_id.

### POST /api/v1/scrape
```json
{ "url": "https://www.example.com/article" }
```

### POST /api/v1/research/data-validity
```json
{
  "keyword": "mortgage rates",
  "goal": "Validate whether the report uses current market data",
  "report_markdown": "...",
  "wait_for_completion": false
}
```
If `wait_for_completion: false`, returns `task_id` + `poll_endpoint`. Poll via `GET /api/v1/research/data-validity/:taskId`.

---

## Recommended First-Test Sequence

```
1. GET  /health
2. POST /api/v1/scrape
3. POST /api/v1/optimize/meta
4. POST /api/v1/audit/content-structure
5. GET  /api/v1/brands/mcclatchy/readiness
6. POST /api/v1/audit/citations
7. GET  /api/v1/jobs/:id  (poll)
```

---

## Common Failures

| Code | Cause |
|------|-------|
| 401 | API key missing, invalid, revoked, or expired |
| 403 | IP allowlist restriction |
| 429 | Rate limit or monthly quota |
| 400 | Missing required field (brand_id, keyword, goal, findings) |
| 500 | Upstream/processing failure — capture body + x-request-id |

---

## Error Reporting to Gary

Send: endpoint called, timestamp (UTC), HTTP status, response body, `x-request-id`, and whether input was `markdown` or `url`.

---

## Planned Endpoints (Not Yet Built)

| Endpoint | Purpose |
|----------|---------|
| `POST /api/v1/audit/ai-overview` | Fetch + summarize Google AI Overview |
| `POST /api/v1/audit/serp-templates` | Top-10 structural patterns from SERP |
| `POST /api/v1/audit/semantic-breadth` | Topical coverage vs. SERP competitors |
| `POST /api/v1/audit/icp-persona` | ICP profile from SERP data |
| `POST /api/v1/audit/forum-insights` | Forum mining for pain points |
| `POST /api/v1/brief/content` | Content brief only (no drafting) |
| `POST /api/v1/report/executive-summary` | High-level summary + top actions |
| `POST /api/v1/report/gap-analysis` | Competitor gap report |
| `POST /api/v1/audit/technical` | Bridge to Tech SEO Agent App |
| `POST /api/v1/optimize/schema` | JSON-LD schema recommendations |
