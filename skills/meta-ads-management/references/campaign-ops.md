# Campaign Operations

Detailed workflows for managing Meta ad campaigns, ad sets, and ads.

## Campaign audit

Get a full picture of an account's campaign structure:

1. List all campaigns:
   ```bash
   meta-ads campaigns list --output table
   ```

2. Filter to active only:
   ```bash
   meta-ads campaigns list --status ACTIVE --output table
   ```

3. Drill into a specific campaign's ad sets:
   ```bash
   meta-ads adsets list --campaign 120210123456789 --output table
   ```

4. See individual ads within an ad set:
   ```bash
   meta-ads ads list --adset 120310123456789 --output table
   ```

## Pausing and activating

Single items:

```bash
meta-ads campaigns pause 120210123456789
meta-ads campaigns activate 120210123456789
meta-ads adsets pause 120310123456789
meta-ads ads pause 120410123456789
```

Bulk operations (multiple IDs at once):

```bash
meta-ads bulk pause --type campaign --ids 123,456,789
meta-ads bulk activate --type adset --ids 123,456
```

## Creating campaigns

```bash
meta-ads campaigns create --name "Q1 Brand Campaign" --objective OUTCOME_AWARENESS
```

Common objectives:
- `OUTCOME_AWARENESS` - brand awareness and reach
- `OUTCOME_TRAFFIC` - drive traffic to a destination
- `OUTCOME_ENGAGEMENT` - post engagement, page likes, event responses
- `OUTCOME_LEADS` - lead generation
- `OUTCOME_APP_PROMOTION` - app installs
- `OUTCOME_SALES` - conversions and catalog sales

## Updating campaigns

```bash
meta-ads campaigns update 120210123456789 --name "Updated Campaign Name"
```

## Bulk export

Export campaign data to a file for offline analysis:

```bash
meta-ads bulk export --type campaigns --status ACTIVE --output-file active-campaigns.json
meta-ads bulk export --type adsets --output-file all-adsets.json
```

## Working with multiple accounts

List available accounts:

```bash
meta-ads accounts list --output table
```

Switch default account:

```bash
meta-ads accounts switch act_987654321
```

Or use `--account` flag on any command to override temporarily:

```bash
meta-ads campaigns list --account act_987654321
```

## Viewing creatives

```bash
meta-ads adcreatives list --output table
meta-ads adcreatives get 120510123456789
```

Creative details include: image URLs, video URLs, body text, titles, call-to-action, and link URLs.
