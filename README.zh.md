# GEO Score — Claude Code 技能

[![License: MIT](https://img.shields.io/badge/License-MIT-22c55e?style=flat-square)](LICENSE)
[![Claude Code](https://img.shields.io/badge/Claude%20Code-skill-d97757?style=flat-square)](https://claude.com/claude-code)
[![GEO](https://img.shields.io/badge/GEO-audit%20%2B%20fix-e84e1b?style=flat-square)](https://growthhunt.ai/geo)

**审计任意网页对 AI 的可见度——然后在你的 AI 编辑器里直接修复。**

[English](README.md) · **中文**

---

AI 回答引擎回答问题时会**引用来源**。如果你的页面没有为它们做好结构，
你就是隐形的：

```
问   “给独立开发者用的最好的 AI 写作工具是什么？”

AI 回答：”最值得考虑的是 Competitor A、Competitor B
         和 Competitor C……”      ← 它们被引用了，你没有。
```

这个技能会审计 AI 引擎能否**抓取、理解并引用**你的页面——然后把安全、确定性的
修复直接应用到你的代码库里。

## 什么是 GEO？

**生成式引擎优化（Generative Engine Optimization）** 是让网页对 AI 回答引擎
可读、可被引用的实践。它不是 SEO：

- **SEO** 优化的是在一列蓝色链接里的排名。
- **GEO** 优化的是被读取、被解析、并**在一段 AI 生成的回答里被引用**。

一个页面可以在 Google 排第一，却对 AI 完全隐形——爬虫被屏蔽、没有结构化数据、
事实密度太低、开头没有直接回答。

## 安装

```bash
npx skills add JoyyyceD/geo-skill
```

或直接 clone 到你的 skills 目录：

```bash
git clone https://github.com/JoyyyceD/geo-skill ~/.claude/skills/geo-audit
```

## 使用

在 Claude Code 里用自然语言说：

> 帮我审计一下落地页的 GEO

> 为什么我的产品在 ChatGPT 里搜不到？

技能会跑一套四步流程：

1. **审计** — 自己抓取页面、自己跑约 45 项检查打 0–100 分。无需 API key、无需账号。
2. **诊断** — 识别你的框架，把每个问题对应到具体文件。
3. **修复** — 应用「生成型」修复，改动前先给你看 diff。
4. **验证** — 你重新部署后再跑一次审计，前后对比。

## 示例

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

## 审计哪些维度

8 个加权维度，约 45 项检查：

| 维度 | 权重 | 检查什么 |
|---|---|---|
| Crawler Access | 13 | OAI-SearchBot / PerplexityBot / ClaudeBot / Google-Extended 能否抓到页面 |
| Indexability & Discovery | 12 | sitemap、canonical、`llms.txt`、RSS——引擎能否发现每个页面 |
| Structure | 15 | 标题层级、列表、FAQ section、语义化 HTML |
| Schema | 12 | JSON-LD 类型、Open Graph 标签、`sameAs` 链接 |
| Factual Density | 13 | 数字、日期、百分比和带来源的论断 |
| Entity Clarity | 10 | 品牌名在 title / H1 / meta / 正文里是否一致 |
| Freshness | 10 | 内容有日期、近期更新过；站点活跃 |
| First Answer | 15 | 前 ~80 词是否直接回答页面主题（LLM 评分） |

另有三个**一票否决项**——AI 爬虫被全屏蔽、整页 `noindex`、页面无法完整分析
（404 或 SPA 空壳）——会直接给总分封顶，不管加权得分多高。

## 它会修什么

✅ **生成型修复** — 自动应用（改动前需你确认）：

- `title`、meta `description`、`canonical`、Open Graph 标签
- JSON-LD 结构化数据（Organization、Article、Product、FAQPage 等）
- `robots.txt` — 放行 AI 爬虫
- `llms.txt` — 根据站点结构生成

❌ **改写型改动** — 只作为建议提出，绝不自动应用：重写首段文案、撰写 FAQ 答案、
改动事实性论断。这些需要你的判断，且有品牌和准确性风险。

技能在写入前一定先展示 diff，绝不自行部署、发布或提交。

## 支持的框架

Next.js（App & Pages Router）、Astro、Hugo、Eleventy，以及纯静态 HTML——
技能会为每种框架定位到正确的文件。

## 常见问题

### 这跟 SEO 审计有什么不同？

SEO 审计查的是排名信号——外链、关键词、Core Web Vitals。这个查的是 AI 回答
引擎能否读取、解析并**引用**你的内容：爬虫权限、结构化数据、事实密度，以及
开头是否直接回答。

### 它会自动改我的网站吗？

不会。每处改动都以 diff 形式提出、等你确认，且只应用确定性的生成型修复。它
不会重写你的文案，不会部署，也不会提交。

### 免费吗？

完全免费。想跑多少次都行。

### 是自包含的吗？

是的。技能自己抓取页面、自己跑全部约 45 项检查——无需 API key、无需账号，
不向任何服务器发送数据。

### 不用 AI 编辑器也能用吗？

可以——[growthhunt.ai/geo](https://growthhunt.ai/geo) 有免费网页版，零配置
快速跑一次审计。

## 相关链接

- **免费网页审计** — [growthhunt.ai/geo](https://growthhunt.ai/geo)
- **GrowthHunt** — [growthhunt.ai](https://growthhunt.ai)

## 许可

MIT — 见 [LICENSE](LICENSE)。
