# Minimal Message Clarity Scorecard MVP

## Overview

Single-page Next.js app that audits website messaging without auth or billing. Paste URL → get instant scorecard with 4 heuristic scores and actionable feedback.

## Architecture

**Stack:**

- Next.js 14 (App Router) + TypeScript
- Tailwind CSS for styling
- OpenAI API (GPT-4o or latest GPT-5 series model)
- `@mozilla/readability` + `jsdom` for content extraction
- Server Actions for audit logic

**No database, no auth** - stateless for now.

## Implementation Steps

### 1. Project Setup

Create Next.js project with:

- `npx create-next-app@latest` with App Router, TypeScript, Tailwind
- Install dependencies: `openai`, `jsdom`, `@mozilla/readability`, `zod`
- Configure `.env.local` with `OPENAI_API_KEY`

### 2. Content Extraction (`/lib/extractor.ts`)

Build function to:

- Fetch HTML from URL (with proper user-agent)
- Parse with `jsdom` + `Readability`
- Return clean text content + metadata (title, description)
- Handle errors (invalid URLs, fetch failures, blocked requests)

### 3. LLM Scoring Engine (`/lib/scorer.ts`)

Create heuristic analyzer:

- Single OpenAI call with structured output (JSON mode or function calling)
- Prompt includes the 4 heuristics with specific 0-5 scoring criteria:
  - **Clarity**: purpose_in_open, reading_level_ok, jargon_density, skimmability
  - **Differentiation**: unique_claim, category_contrast, specificity
  - **Proof**: social_proof, quant_metrics, risk_reversal, demo_cta
  - **Emotion**: vivid_words, audience_specific, benefit_first
- Returns scores + issues array with {type, quote, explanation, severity}
- Calculate overall score (0-100) by averaging all signals

### 4. API Route (`/app/api/audit/route.ts`)

Server Action or POST endpoint:

```typescript
POST /api/audit
Body: { url: string, pageType?: "home" | "product" | "pricing" }
Response: { 
  overall: number,
  subscores: { clarity, differentiation, proof, emotion },
  issues: [{ signal, quote, explanation, severity }],
  metadata: { title, url }
}
```

### 5. UI Components (`/app/page.tsx` + components)

**Landing/Audit Page:**

- Hero with value prop + URL input field
- Page type selector (optional: home/product/pricing)
- "Audit" button → loading state → results

**Results Display:**

- Overall score gauge (0-100, color-coded)
- 4 subscore cards with individual scores
- Issues list grouped by severity (high/medium/low)
- Export button (download JSON)

**Styling:**

- Clean, modern design with Tailwind
- Responsive layout
- Score visualizations (progress rings or bars)

### 6. Error Handling & Polish

- Loading states with skeleton UI
- Error messages for failed fetches or invalid URLs
- Rate limiting feedback (OpenAI API limits)
- Mobile-responsive layout

## File Structure

```
/app
  /api/audit/route.ts          # Audit endpoint
  page.tsx                       # Main landing + results page
  layout.tsx                     # Root layout
/components
  AuditForm.tsx                  # URL input + submit
  ScoreCard.tsx                  # Overall score display
  HeuristicCard.tsx              # Individual heuristic scores
  IssuesList.tsx                 # Issues with severity
/lib
  extractor.ts                   # Content extraction logic
  scorer.ts                      # OpenAI scoring engine
  types.ts                       # TypeScript interfaces
.env.local                       # OPENAI_API_KEY
```

## Success Criteria

- User can paste any public URL and get results in <10 seconds
- Scores are meaningful and issues are actionable
- Clean, professional UI that works on mobile
- Graceful error handling for edge cases
