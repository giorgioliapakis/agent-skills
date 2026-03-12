# Keyword Research Workflows

Detailed guidance for keyword research tasks using `dfs volume`, `dfs suggestions`, `dfs related`, and `dfs difficulty`.

## Seed keyword expansion

Start with a seed term and expand outward:

1. Check the seed: `dfs volume "your keyword" --table`
2. Get suggestions: `dfs suggestions "your keyword" -n 20 --table`
3. Get related terms: `dfs related "your keyword" -n 20 --table`
4. Check difficulty on the best candidates: `dfs difficulty "kw1" "kw2" "kw3"`

Suggestions come from autocomplete data (what people actually type). Related terms come from semantic analysis (conceptually similar). Use both to get full coverage.

## Content brief keyword research

When building a content brief, gather primary + secondary + long-tail keywords:

1. `dfs volume "primary keyword"` - confirm the main target has volume
2. `dfs suggestions "primary keyword" -n 30` - find secondary keywords and long-tail variations
3. `dfs related "primary keyword" -n 20` - find semantic angles to cover
4. `dfs volume "secondary1" "secondary2" "longtail1" "longtail2"` - validate the best candidates
5. `dfs serp "primary keyword" --json` - check what content types rank (guides, listicles, tools)

Group the results by intent (informational, commercial, navigational) to plan content structure.

## Bulk volume checks

`dfs volume` accepts up to 50 keywords in one call:

```bash
dfs volume "keyword 1" "keyword 2" "keyword 3" ... "keyword 50" --table
```

Use this when you have a list of candidates and need to quickly filter by volume and difficulty.

## Interpreting difficulty scores

| Difficulty | Meaning | Strategy |
|-----------|---------|----------|
| 0-20 | Very easy | New sites can rank with decent content |
| 21-40 | Easy | Good content + basic on-page SEO |
| 41-60 | Medium | Need quality content + some backlinks |
| 61-80 | Hard | Need authority, strong content, link building |
| 81-100 | Very hard | Dominated by major brands, avoid unless you're one |

## Interpreting competition

Competition (LOW/MEDIUM/HIGH) reflects Google Ads advertiser competition, not organic difficulty. A keyword can have LOW competition (few advertisers) but HIGH difficulty (hard to rank organically).

## Location and language targeting

Default is US English. For other markets:

```bash
dfs locations sweden        # find the code
dfs languages swedish       # find the code
dfs volume "seo verktyg" --location 2752 --language sv --table
```

Common location codes: US (2840), UK (2826), Australia (2036), Canada (2124), Germany (2276).
