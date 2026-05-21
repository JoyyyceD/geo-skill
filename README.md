# GEO Score — a Claude Code skill

[![License: MIT](https://img.shields.io/badge/License-MIT-22c55e?style=flat-square)](LICENSE)
[![Claude Code](https://img.shields.io/badge/Claude%20Code-skill-d97757?style=flat-square)](https://claude.com/claude-code)
[![GEO](https://img.shields.io/badge/GEO-audit%20%2B%20fix-e84e1b?style=flat-square)](https://growthhunt.ai/geo)

**Audit any web page for AI search visibility — then apply the fixes, right inside Claude Code.**

**English** · [中文](README.zh.md)

---

AI answer engines — ChatGPT, Perplexity, Gemini, Claude — answer questions by
**citing sources**. If your pages aren't structured for them, you're invisible:

```
Q   "What's the best AI writing tool for solo founders?"

Perplexity:  "The strongest options are Competitor A, Competitor B
              and Competitor C…"      ← they get cited. You don't.
```

This skill audits whether AI engines can **crawl, understand and cite** your
page — then applies the safe, deterministic fixes in your codebase.

## What is GEO?

**Generative Engine Optimization** is the practice of making web pages legible
and citable to AI answer engines. It is not SEO:

- **SEO** optimizes for ranking in a list of blue links.
- **GEO** optimizes for being read, parsed and **cited inside a single
  AI-generated answer**.

A page can rank #1 on Google and still be invisible to AI — blocked crawlers,
no structured data, thin factual density, no direct answer up top.

## Install

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

The skill runs a four-step workflow:

1. **Audit** — scores the URL 0–100 via the free GrowthHunt GEO API.
2. **Diagnose** — detects your framework and maps each issue to a file.
3. **Fix** — applies generation-type fixes with a diff you approve.
4. **Verify** — re-runs the audit after you redeploy, and compares.

## Example

```
GEO Score   61 / 100  (C)
AI visibility    ChatGPT ◐    Perplexity ●    Gemini ◐    Claude ○

  Crawler Access             96%   ████████████████████░
  Indexability & Discovery   58%   ████████████░░░░░░░░░
  Structure                  72%   ███████████████░░░░░░
  Schema                     40%   ████████░░░░░░░░░░░░░
  Factual Density            36%   ████████░░░░░░░░░░░░░
  Entity Clarity             80%   █████████████████░░░░
  Freshness                  50%   ███████████░░░░░░░░░░
  First Answer               30%   ██████░░░░░░░░░░░░░░░

Priority fixes
  1  [high]  Add /llms.txt so AI crawlers can map your site
  2  [high]  Rewrite the opening 80 words to answer the page topic
  3  [med]   Add Product + FAQPage JSON-LD
  4  [med]   Add an FAQ section with question-style H2s
```

## What it scores

8 weighted dimensions, ~45 checks:

| Dimension | Weight | What it measures |
|---|---|---|
| Crawler Access | 13 | Can OAI-SearchBot, PerplexityBot, ClaudeBot and Google-Extended fetch the page? |
| Indexability & Discovery | 12 | sitemap, canonical, `llms.txt` and RSS — can engines find every page? |
| Structure | 15 | Heading hierarchy, lists, an FAQ section, semantic HTML |
| Schema | 12 | JSON-LD types, Open Graph tags, `sameAs` links |
| Factual Density | 13 | Numbers, dates, percentages and sourced claims |
| Entity Clarity | 10 | Brand named consistently across title, H1, meta and copy |
| Freshness | 10 | Dated, recently-updated content; an actively-updated site |
| First Answer | 15 | Do the first ~80 words directly answer the page topic? (LLM-scored) |

Three **gating flags** — all AI bots blocked, page `noindex`, page not
analyzable (404 or client-rendered shell) — cap the score regardless of the
weighted total.

## What it fixes

✅ **Generation-type fixes** — applied automatically, with your approval:

- `title`, meta `description`, `canonical`, Open Graph tags
- JSON-LD structured data (Organization, Article, Product, FAQPage…)
- `robots.txt` — unblock AI crawlers
- `llms.txt` — generated from your site structure

❌ **Rewrite-type changes** — surfaced as recommendations, never auto-applied:
rewriting hero copy, writing FAQ answers, changing factual claims. These need
your judgement and carry brand/accuracy risk.

The skill always shows a diff before writing, and never deploys, publishes or
commits on its own.

## Supported frameworks

Next.js (App & Pages Router), Astro, Hugo, Eleventy, and plain static HTML —
the skill locates the right files for each.

## FAQ

### How is this different from an SEO audit?

An SEO audit checks ranking signals — backlinks, keywords, Core Web Vitals.
This checks whether an AI answer engine can read, parse and **cite** your
content: crawler permissions, structured data, factual density, and a direct
first answer.

### Does it change my site automatically?

No. It proposes every change as a diff and waits for your approval, and only
applies deterministic, generation-type fixes. It never rewrites your copy,
deploys, or commits.

### Is it free?

Yes. The skill and the underlying audit API are free. Run it as often as you
like from Claude Code.

### Does it work without Claude Code?

The audit does — run it free at [growthhunt.ai/geo](https://growthhunt.ai/geo).
The file-locating and fixing workflow needs Claude Code.

## Links

- **Free web audit** — [growthhunt.ai/geo](https://growthhunt.ai/geo)
- **GrowthHunt** — [growthhunt.ai](https://growthhunt.ai)

## License

MIT — see [LICENSE](LICENSE).
