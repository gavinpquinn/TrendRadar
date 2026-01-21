# TrendRadar Setup - Mindset Consulting

SAP/BTP industry news and competitor monitoring via GitHub Actions.

## Quick Links

- **GitHub Repo**: https://github.com/gavinpquinn/TrendRadar
- **Actions Dashboard**: https://github.com/gavinpquinn/TrendRadar/actions
- **Workflow Runs**: https://github.com/gavinpquinn/TrendRadar/actions/workflows/crawler.yml

## Schedule

Runs automatically **twice daily** at:
- 7:00 AM Central Time
- 5:00 PM Central Time

## How to Update Keywords

Edit `config/frequency_words.txt`:

```
[Group Name]
keyword1
keyword2
/regex pattern/i
```

Current keyword groups:
- **SAP Products**: BTP, Datasphere, S/4HANA, Integration Suite, SAP Build, etc.
- **Competitors**: IBM, Accenture, Deloitte, Capgemini, Infosys, Wipro, TCS
- **Trends**: ERP modernization, cloud migration, enterprise AI, data integration

## How to Change Notification Settings

### Slack Webhook
Update the secret in GitHub:
1. Go to https://github.com/gavinpquinn/TrendRadar/settings/secrets/actions
2. Edit `SLACK_WEBHOOK_URL`

### Add Email Notifications
Add these secrets:
- `EMAIL_FROM` - sender email address
- `EMAIL_PASSWORD` - app password (for Gmail, create at https://myaccount.google.com/apppasswords)
- `EMAIL_TO` - recipient email(s), comma-separated

## How to Manually Trigger a Run

**Option 1: GitHub UI**
1. Go to https://github.com/gavinpquinn/TrendRadar/actions/workflows/crawler.yml
2. Click "Run workflow" button

**Option 2: CLI**
```bash
gh workflow run crawler.yml --repo gavinpquinn/TrendRadar
```

## How to Change Schedule

Edit `.github/workflows/crawler.yml`, update the cron lines:
```yaml
- cron: "0 13 * * *"   # 7:00 AM CT (13:00 UTC)
- cron: "0 23 * * *"   # 5:00 PM CT (23:00 UTC)
```

Cron format: `minute hour day month weekday` (UTC time)

## Where to View Logs

1. Go to https://github.com/gavinpquinn/TrendRadar/actions
2. Click on a workflow run
3. Click "crawl" job to see detailed logs

## RSS Feeds Configured

| Source | Category |
|--------|----------|
| Hacker News | Tech News |
| TechCrunch | Tech News |
| The Verge | Tech News |
| Ars Technica | Tech News |
| Reuters Business | Business |
| Bloomberg Technology | Business |
| SAP News | SAP Official |
| SAP Community Blogs | SAP Official |
| ZDNet | Enterprise Tech |
| InfoWorld | Enterprise Tech |
| Computerworld | Enterprise Tech |

## Trial Mode Note

GitHub Actions has a 7-day trial cycle. To continue:
1. Go to Actions tab
2. Run the "Check In" workflow before the 7 days expire

For long-term use, consider Docker deployment.

## Troubleshooting

**No notifications received?**
- Check workflow completed successfully in Actions tab
- Verify Slack webhook URL is correct in secrets
- Check Slack channel permissions

**Workflow failing?**
- View logs in Actions tab
- Common issues: RSS feed URLs changed, rate limiting

## Adding More RSS Feeds

Edit `config/config.yaml` under the `rss.feeds` section:
```yaml
- id: "unique-id"
  name: "Display Name"
  url: "https://example.com/feed.xml"
```
