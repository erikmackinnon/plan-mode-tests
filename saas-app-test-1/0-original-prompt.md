Create a plan for this app. (or "Use the predev fast-spec to create a plan for this app")

Build a self‑serve “message clarity scorecard” for solo founders and small teams using the Wynter messaging framework.

---

# The concept (why it matters)

Most small sites never get a sanity check on their copy. Your app lets anyone paste a URL and instantly get a scorecard across 4 heuristics—**Clarity, Differentiation, Proof, Emotion**—plus quick fixes. Think “Grammarly for positioning.”

---

# Pricing

* **Starter — $29/mo**: unlimited audits on 1 domain, CSV/PDF export, shareable links.
* **Pro — $59/mo**: 5 domains, history + deltas, webhook, basic brand terms library.
* **Add‑on — Brand Tracking $99/mo**: weekly crawl of key pages + score trends, alerting, “share of message” diff vs 3 competitors (paste their URLs).

---

# UX in 5 steps

1. Paste URL → choose page type (home, product, pricing)
2. Click “Audit” → run fetch → extract main content → run heuristics
3. Show **overall score (0–100)** + 4 subscores + top issues + suggested rewrites
4. “Before/After” inline edits (single‑click apply)
5. Save to project → trend over time → export/share

---

# Heuristics (LLM prompts + lightweight rules)

* **Clarity**: jargon density, sentence length, reading level, purpose clarity in first 50–80 words.
* **Differentiation**: unique value vs “category boilerplate,” presence of a sharp “only we” angle, comparative specifics.
* **Proof**: logos, metrics, testimonials with sources, concrete numbers, demos/trials present.
* **Emotion**: vivid language, audience resonance, urgency, risk reversal, voice consistency.

**Scoring rubric (0–5 each signal; normalize to 100):**

```json
{
  "clarity": {"purpose_in_open":0-5,"reading_level_ok":0-5,"jargon_density":0-5,"skimmability":0-5},
  "differentiation": {"unique_claim":0-5,"category_contrast":0-5,"specificity":0-5},
  "proof": {"social_proof":0-5,"quant_metrics":0-5,"risk_reversal":0-5,"demo_cta":0-5},
  "emotion": {"vivid_words":0-5,"audience_specific":0-5,"benefit_first":0-5}
}
```

---

# Tech in a weekend (Next.js + Vercel)

* **Frontend**: Next.js (app router), Tailwind, Server Actions for audits, React Hook Form.
* **Backend**: Next API routes; `node-fetch` + Readability to extract content; OpenAI Responses API for heuristic scoring + rewrite suggestions.
* **DB**: SQLite (Turso/LibSQL) or Supabase (projects, pages, runs).
* **Auth & Billing**: Clerk/NextAuth + Stripe Checkout & Billing (metered optional).
* **Jobs**: Vercel cron for weekly brand tracking; queue via Upstash Redis if needed.

**Tables (minimal)**

```sql
projects(id, user_id, name, domain)
pages(id, project_id, url, page_type)
audits(id, page_id, created_at, overall, clarity, differentiation, proof, emotion, json_blob)
competitors(id, project_id, url)
```

---

# API shape

```http
POST /api/audit
Body: { url, pageType?, competitorUrls?: string[] }
Res:  { overall, subscores:{clarity, differentiation, proof, emotion}, issues:[{type, why, severity}], rewrites:[{section, before, after}] }
```

---

# LLM prompt sketch (per heuristic)

```
You are a brutal messaging analyst. Given CLEAN_TEXT and PAGE_TYPE, score 0–5 for each signal.
Return strict JSON {scores:{...}, issues:[{signal,quote,explanation,fix}], rewrites:[{section,before,after}]}.
Guidelines: penalize clichés, reward specifics, quantify proof, keep rewrites <= 2 sentences each.
```

---

# Brand tracking add‑on (how it works)

* Weekly crawl: `/`, `/product`, `/pricing`, top blog post.
* Store scores; compute **deltas**; email/Slack alert if change > ±8 or if competitor surpasses any subscore.
* “Share of message” diff: build a tiny terms library (e.g., “AI safety,” “B2B buyer panel,” “instant insights”) → show frequency vs competitors and movement over time.
