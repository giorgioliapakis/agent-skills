# Performance Insights

Detailed workflows for pulling Meta Ads performance data, analyzing metrics, and using breakdowns.

## Basic performance pull

Get campaign-level performance for the last 7 days:

```bash
meta-ads insights get --level campaign --date-preset last_7d
```

Levels: `campaign`, `adset`, `ad`

## Date presets

| Preset | Period |
|--------|--------|
| `today` | Today |
| `yesterday` | Yesterday |
| `last_3d` | Last 3 days |
| `last_7d` | Last 7 days |
| `last_14d` | Last 14 days |
| `last_30d` | Last 30 days |
| `last_90d` | Last 90 days |
| `this_month` | Current month |
| `last_month` | Previous month |

## Custom date ranges

```bash
meta-ads insights get --level campaign --date-range 2025-01-01:2025-01-31
meta-ads insights get --level ad --date-range 2025-03-01:2025-03-07
```

Format: `YYYY-MM-DD:YYYY-MM-DD`

## Breakdowns

Add demographic and placement breakdowns:

```bash
# Age breakdown
meta-ads insights get --level adset --date-preset last_7d --breakdowns age

# Age and gender combined
meta-ads insights get --level adset --date-preset last_30d --breakdowns age,gender

# Platform breakdown (Facebook vs Instagram)
meta-ads insights get --level campaign --date-preset last_7d --breakdowns publisher_platform

# Placement breakdown
meta-ads insights get --level ad --date-preset last_7d --breakdowns platform_position
```

Common breakdowns: `age`, `gender`, `country`, `region`, `publisher_platform`, `platform_position`, `device_platform`, `impression_device`

## Performance analysis workflow

### Weekly account review

1. Get campaign-level metrics:
   ```bash
   meta-ads insights get --level campaign --date-preset last_7d --output table
   ```

2. Identify top/bottom performers by drilling into ad set level:
   ```bash
   meta-ads insights get --level adset --date-preset last_7d --output table
   ```

3. Check demographic performance:
   ```bash
   meta-ads insights get --level adset --date-preset last_7d --breakdowns age,gender
   ```

### Creative performance review

1. Get ad-level insights:
   ```bash
   meta-ads insights get --level ad --date-preset last_14d
   ```

2. Cross-reference with creatives:
   ```bash
   meta-ads adcreatives list
   ```

3. Identify winning creative elements by comparing ad performance with their creative details.

### Month-over-month comparison

Pull two months and compare:

```bash
meta-ads insights get --level campaign --date-range 2025-02-01:2025-02-28
meta-ads insights get --level campaign --date-range 2025-03-01:2025-03-31
```

Parse the JSON output to calculate deltas on key metrics (spend, impressions, clicks, conversions, CPA).

## Key metrics in output

The insights response includes: impressions, clicks, spend, reach, frequency, cpc, cpm, ctr, conversions, cost_per_conversion, and more depending on the campaign objective and available data.
