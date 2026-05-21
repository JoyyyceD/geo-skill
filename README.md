# GEO Audit — a Claude Code skill

Audit any web page for **GEO (Generative Engine Optimization)** and apply the
fixes directly in your codebase — so ChatGPT, Perplexity, Gemini and Claude can
crawl, understand and **cite** your pages.

Built by [GrowthHunt](https://growthhunt.ai). Powered by the free audit at
**[growthhunt.ai/geo](https://growthhunt.ai/geo)**.

## What is GEO?

GEO is the practice of making web pages legible and citable to AI answer
engines. SEO optimizes for ranking in a list of blue links; GEO optimizes for
being read, understood and **cited inside a single AI-generated answer**. A page
can rank #1 on Google and still be invisible to AI — blocked crawlers, no
structured data, thin factual density, no direct answer up top.

## Install

**Claude Code:**

```bash
npx skills add JoyyyceD/geo-skill
```

Or clone it straight into your skills directory:

```bash
git clone https://github.com/JoyyyceD/geo-skill ~/.claude/skills/geo-audit
```

## Usage

In Claude Code, just ask in plain language:

> Audit my landing page for GEO

> Why isn't my product showing up in ChatGPT?

The skill audits the URL, shows you a 0–100 score and the prioritized issues,
then offers to apply the **generation-type fixes** — title/meta tags, JSON-LD
schema, `robots.txt`, `llms.txt` — in your repo, with a diff you approve before
anything is written. It never deploys, publishes or commits on its own.

## What it scores

The audit runs **8 weighted dimensions** across roughly **45 checks**:

| Dimension | Weight | What it measures |
|---|---|---|
| Crawler Access | 13 | Can OAI-SearchBot, PerplexityBot, ClaudeBot and Google-Extended fetch the page? |
| Indexability & Discovery | 12 | sitemap, canonical, `llms.txt`, RSS |
| Structure | 15 | Heading hierarchy, lists, an FAQ section, semantic HTML |
| Schema | 12 | JSON-LD types, Open Graph, `sameAs` |
| Factual Density | 13 | Numbers, dates and sourced claims |
| Entity Clarity | 10 | Brand named consistently across title, H1 and copy |
| Freshness | 10 | Dated, recently-updated content |
| First Answer | 15 | Do the first ~80 words directly answer the page topic? |

Three gating flags (all AI bots blocked, page `noindex`, page not analyzable)
cap the score regardless of the weighted total.

## FAQ

### How is this different from an SEO audit?

SEO audits check ranking signals — backlinks, keywords, Core Web Vitals. This
checks whether an AI answer engine can read, parse and cite your content:
crawler permissions, structured data, factual density, and a direct first answer.

### Does it change my site automatically?

No. It proposes fixes as diffs and waits for your approval. It only applies
deterministic, generation-type fixes — it never rewrites your copy or publishes.

### Is it free?

Yes. The skill and the underlying audit API are free. Run it as often as you
like from Claude Code.

### What frameworks does it support?

Next.js (App and Pages Router), Astro, Hugo, Eleventy, and plain static HTML —
the skill locates the right files for each.

## Links

- **Free web audit:** [growthhunt.ai/geo](https://growthhunt.ai/geo)
- **GrowthHunt:** [growthhunt.ai](https://growthhunt.ai)
