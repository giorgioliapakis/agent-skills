# SERP Analysis Workflows

Detailed guidance for analyzing search results and page content using `dfs serp` and `dfs content`.

## Analyzing a SERP

```bash
dfs serp "best seo tools" --target yourdomain.com --table
```

The output has two parts:
- **stderr**: SERP features detected (ai_overview, featured_snippet, people_also_ask, video, images) + your target's position if found + PAA questions
- **stdout**: organic results with position, domain, title, URL

Use `--json` for the full structured result when you need to parse features or PAA questions programmatically.

## SERP feature detection

Features tell you what Google considers the right content format for a query:

| Feature | What it means | Content implication |
|---------|--------------|---------------------|
| ai_overview | Google shows an AI-generated summary | Need clear, structured answers that AI can cite |
| featured_snippet | A highlighted answer box | Structure content with direct answers, lists, tables |
| people_also_ask | Related questions shown | Cover these questions in your content |
| video | Video results in SERP | Consider video content for this query |
| images | Image pack shown | Include relevant images, optimize alt text |

## Content gap analysis

Compare your page against top-ranking competitors:

1. `dfs serp "target keyword" --json` - see who ranks and what features appear
2. `dfs content "https://competitor1.com/page" --full --json` - get their headings and word count
3. `dfs content "https://competitor2.com/page" --full --json` - compare another competitor
4. `dfs content "https://yoursite.com/page" --full --json` - compare against your own page

Look for:
- Word count gaps (are competitors writing longer/shorter?)
- Heading structure differences (what topics do they cover that you don't?)
- Missing sections that top rankers all include

## PAA (People Also Ask) research

PAA questions from `dfs serp --json` are valuable for:
- FAQ sections on your page
- Subheadings that directly answer questions
- Related content ideas

Run SERP analysis on 3-5 related keywords to build a comprehensive PAA list for a topic.

## Multi-keyword SERP comparison

When evaluating a topic cluster, analyze SERPs for multiple related keywords:

```bash
dfs serp "seo tools" --table
dfs serp "best seo tools" --table
dfs serp "seo tools for small business" --table
```

Compare which domains appear across multiple SERPs - these are your real competitors for the topic, not just a single keyword.
