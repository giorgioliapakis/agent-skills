# Competitor Intelligence Workflows

Detailed guidance for competitor analysis using `dfs ranked`, `dfs overlap`, and `dfs competitors`.

## Domain keyword audit

See what keywords a domain ranks for, sorted by volume:

```bash
dfs ranked ahrefs.com -n 30 --table
```

Returns: `keyword, position, volume, cpc, url`

Use this to understand a competitor's keyword portfolio - what they target, where they rank, and which pages drive their organic traffic.

## Domain overlap analysis

Compare keyword rankings between two domains:

```bash
dfs overlap ahrefs.com semrush.com -n 30 --table
```

Returns: `keyword, pos1, pos2, volume, cpc`

This shows keywords both domains rank for with their respective positions. Use it to find:
- Keywords where you rank lower than a competitor (catch-up opportunities)
- Keywords where you rank higher (defend these positions)
- High-volume keywords where both rank poorly (opportunity for both)

## Finding SERP competitors

Discover which domains compete for a set of keywords:

```bash
dfs competitors "seo tools" "keyword research tool" "backlink checker" -n 10 --table
```

Returns: `domain, avg_position, visibility, keywords_count`

Pass your target keywords and see who shows up most. This is different from `dfs ranked` (which starts from a domain) - this starts from keywords and finds the domains.

## Full competitor research workflow

When analyzing a competitor from scratch:

1. **Map their keyword portfolio:**
   ```bash
   dfs ranked competitor.com -n 50 --table
   ```
   Look at which keywords drive the most volume and which URLs appear most.

2. **Compare against your domain:**
   ```bash
   dfs overlap yoursite.com competitor.com -n 30 --table
   ```
   Find gaps where they rank and you don't, or where you're close but behind.

3. **Deep dive on key terms:**
   ```bash
   dfs serp "their top keyword" --target yoursite.com --table
   ```
   See the full SERP landscape for their best keywords.

4. **Analyze their top pages:**
   ```bash
   dfs content "https://competitor.com/their-top-page" --full --json
   ```
   Understand their content structure and find gaps to exploit.

## Competitive landscape mapping

To understand an entire market, start from keywords rather than domains:

1. `dfs competitors "primary keyword 1" "primary keyword 2" -n 15` - find all competitors
2. `dfs ranked <top-competitor> -n 20` - map each competitor's keyword strategy
3. `dfs overlap <you> <competitor> -n 20` - find gaps for each competitor

Build a matrix of keywords vs. competitors to identify where the biggest opportunities are.
