# Geo Content Generator

> **Agent**: `depositback-agent-geo-content-generator`  
> **Group**: Content Production (Group 2)  
> **Product**: DepositBack — Security Deposit Demand Letter Service  
> **Price Points**: $19.99 (demand letter) / $39.99 (small claims prep)

## Purpose

Creates localized, AI-search-optimized content for all 50 US states. Produces FAQ pages, HowTo guides, state law comparison tables, penalty calculators, and schema markup (FAQPage, HowTo, Article) to maximize citation in ChatGPT, Perplexity, and Google AI Overviews.

## DepositBack Context

DepositBack is a single-page, no-signup transactional product for US renters seeking to recover security deposits. The entire customer journey fits on one URL: landing page → 6-question form → Revolut payment → PDF emailed. Conversion rate target: **4% visitor-to-purchase minimum** (median for sub-$60 e-commerce). Content must be state-specific, CCPA-compliant, and optimized for both traditional SEO and Generative Engine Optimization (GEO).

## Inputs (from Group 1 — Discovery)

- Pain signals from pain-signal-monitor (tenant complaints by state)
- Search intents from search-intent-scanner (state + deposit keywords)
- Competitor intel from competitor-review-miner (gaps in content)

## Outputs (to Group 3 — Distribution)

- State blog posts + schema → distribution/seo-optimizer inbox
- FAQPage JSON-LD → distribution/schema-deployer inbox
- Penalty calculator copy → distribution/web-integrator inbox

## Human Escalation Points 🛑

- Legal review required for statutory language (CA Civ. Code §1950.5, etc.)
- Citation accuracy for state law references
- First 20 published pieces need human QA

## Skills

| Skill | Description | Status |
|-------|-------------|--------|
| `noop` | Health check / pipeline verification | ✅ Active |
| `generate` | Primary content generation for this agent | 🔧 Planned |

## Workflow

1. Poll `data/inbox/` for task manifests from upstream agents.
2. Resolve required skills (local `skills/` or ClawHub fallback).
3. Execute content generation workflow.
4. Write artifacts to `data/outbox/`.
5. Update `data/state.json` with status and artifact references.

## Inter-Agent Protocol

```
Discovery (Group 1) → [THIS AGENT] → Distribution (Group 3)
     pain-signals    →   generates    →   publishes
     search-intents  →   content      →   distributes
     competitor-intel→   assets       →   amplifies
```

## Runtime

```bash
pip install -r requirements.txt
python runtime/main.py
```

## Secrets Required

- `MOONSHOT_API_KEY` — AI content generation
- `GITHUB_TOKEN` — Auto-provided for Actions
