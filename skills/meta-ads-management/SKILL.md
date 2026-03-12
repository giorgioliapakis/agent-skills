---
name: meta-ads-management
description: |
  Meta (Facebook/Instagram) Ads campaign management, insights, and bulk operations via the
  meta-ads CLI. Lists campaigns, ad sets, and ads, pulls performance insights with breakdowns,
  pauses/activates items, and exports data. Use when asked about Meta ad performance, campaign
  management, ad creative review, audience breakdowns, or bulk ad operations.
  Requires: npm install -g meta-ads-cli
---

# Meta Ads Management

Manage Meta (Facebook/Instagram) Ads accounts via the `meta-ads` CLI. Structured JSON output by default, designed for agent workflows.

## Prerequisites

```bash
npm install -g meta-ads-cli
```

## Auth

Check auth status:

```bash
meta-ads auth status
```

If not authenticated:

```bash
meta-ads auth login --token YOUR_ACCESS_TOKEN
# Or interactive:
meta-ads auth login
```

Tokens come from Meta Business Suite > Business Settings > System Users. Needs `ads_management` and `ads_read` permissions.

## Set default account

```bash
meta-ads accounts list
meta-ads accounts switch act_123456789
```

## Choosing the right command

| Need | Command | When to use |
|------|---------|-------------|
| List ad accounts | `meta-ads accounts list` | Find account IDs, switch between accounts |
| View campaigns | `meta-ads campaigns list` | See all campaigns, filter by status |
| Campaign details | `meta-ads campaigns get <id>` | Deep dive on a specific campaign |
| Pause/activate campaigns | `meta-ads campaigns pause/activate <id>` | Toggle campaign status |
| Create a campaign | `meta-ads campaigns create` | Set up new campaign with objective |
| View ad sets | `meta-ads adsets list` | See ad sets, filter by campaign |
| View ads | `meta-ads ads list` | See individual ads, filter by ad set |
| View creatives | `meta-ads adcreatives list` | See creative assets and copy |
| Performance data | `meta-ads insights get` | Metrics by campaign/adset/ad level with date ranges |
| Bulk operations | `meta-ads bulk` | Pause/activate/export multiple items at once |

## Commands

### Campaigns

```bash
meta-ads campaigns list
meta-ads campaigns list --status ACTIVE
meta-ads campaigns list --output table
meta-ads campaigns get 120210123456789
meta-ads campaigns create --name "Q1 Brand" --objective OUTCOME_AWARENESS
meta-ads campaigns update 120210123456789 --name "Updated Name"
meta-ads campaigns pause 120210123456789
meta-ads campaigns activate 120210123456789
```

### Ad Sets

```bash
meta-ads adsets list
meta-ads adsets list --campaign 120210123456789
meta-ads adsets get 120310123456789
meta-ads adsets pause 120310123456789
meta-ads adsets activate 120310123456789
```

### Ads

```bash
meta-ads ads list
meta-ads ads list --adset 120310123456789
meta-ads ads get 120410123456789
meta-ads ads pause 120410123456789
meta-ads ads activate 120410123456789
```

### Ad Creatives

```bash
meta-ads adcreatives list
meta-ads adcreatives get 120510123456789
```

### Insights

```bash
meta-ads insights get --level campaign --date-preset last_7d
meta-ads insights get --level ad --date-range 2025-01-01:2025-01-31
meta-ads insights get --level adset --breakdowns age,gender
```

### Bulk Operations

```bash
meta-ads bulk pause --type campaign --ids 123,456,789
meta-ads bulk activate --type adset --ids 123,456
meta-ads bulk export --type campaigns --status ACTIVE --output-file campaigns.json
```

## Output formats

Default is JSON (structured for agent parsing). Use `--output table` when presenting to users.

## Global flags

```
-a, --account   Ad account ID (overrides default)
-o, --output    Output format (json/table)
-v, --verbose   Enable verbose output
-q, --quiet     Suppress non-essential output
```

## Configuration priority

1. Command flags (highest)
2. Environment variables (`META_ADS_ACCESS_TOKEN`, `META_ADS_ACCOUNT_ID`, etc.)
3. Config file (`~/.config/meta-ads/config.json`)

## Workflow references

For detailed workflows and common operations:

| Task | Reference |
|------|-----------|
| Campaign management, status changes, bulk operations | [references/campaign-ops.md](references/campaign-ops.md) |
| Performance analysis, insights, breakdowns | [references/insights.md](references/insights.md) |

Read only the reference you need for the current task.
