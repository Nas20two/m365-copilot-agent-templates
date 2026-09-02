# AI Spend Dashboard — Test Data

Sample transaction data and usage reports for validating the workflow's AI classify node, aggregation logic, and outlier detection.

---

## Sample Spend & Usage Data

### Dataset 1: Balanced Spend (Baseline)

| Team | Department | $/user | Users | Total | Productive Activity | Notes |
|---|---|---|---|---|---|---|
| Engineering | Product | $245 | 12 | $2,940 | 154 PRs merged, 34 deploys | Normal AI-assisted dev |
| Marketing | GTM | $180 | 8 | $1,440 | 12 campaign drafts, 42 content pieces | Content generation — productive |
| Sales | Revenue | $320 | 15 | $4,800 | 87 email sequences, 22 proposals | Sales acceleration — productive |
| Support | Ops | $95 | 6 | $570 | 340 ticket responses | Support efficiency — productive |

**Expected classification:** All Productive
**Outlier flag:** None (all under $500/user)

---

### Dataset 2: Shadow IT Signals

| Team | Department | $/user | Users | Total | Productive Activity | Notes |
|---|---|---|---|---|---|---|
| Engineering | Product | $210 | 12 | $2,520 | 89 PRs, 21 deploys | Normal |
| Marketing | GTM | $890 | 8 | $7,120 | 3 campaign drafts, 0 published | 🔴 Heavy spend, no output |
| Finance | Ops | $45 | 4 | $180 | 12 reconciliation reports | Normal (low) |
| Growth Lab | R&D | $1,200 | 5 | $6,000 | No measurable output, no tickets | 🔴 Shadow IT candidate |

**Expected classification:**
- Marketing: Experimental (spending but minimal output)
- Growth Lab: Shadow IT (heavy spend, zero measurable output)

**Outlier flag:** Marketing + Growth Lab ≥ $500/user threshold

---

### Dataset 3: Executive Dashboard Scenario

| Team | Department | $/user | Users | Total | Productive Activity | Notes |
|---|---|---|---|---|---|---|
| Data Science | Product | $420 | 8 | $3,360 | 45 models trained, 12 deployed | High output, justifies spend |
| Engineering | Product | $510 | 20 | $10,200 | 312 PRs, 67 deploys | Borderline per-user, high volume |
| Legal | Ops | $60 | 4 | $240 | 12 contract reviews | Baseline |
| Executive | Leadership | $1,800 | 2 | $3,600 | Strategy docs, board prep | 🟡 High per-user cost — review |
| Customer Success | Revenue | $280 | 14 | $3,920 | 860 customer interactions | Productive — high volume justifies |

**Expected classification:**
- Data Science: Productive (high output)
- Engineering: Productive (high volume justifies per-user cost)
- Executive: Experimental (high per-user expense needs scrutiny)
- Customer Success: Productive (high interaction volume)
- Legal: Productive

**Outlier flag:** Executive flagged (≥$500/user, low measurable output)
**Aggregate metrics:**
- Total spend: $21,320
- Avg $/user: ~$240
- Most efficient: Legal ($60/user, high-value reviews)

---

### Validation Steps

1. Import the workflow YAML into Copilot Studio.
2. Configure connection references (HTTP, SharePoint, Teams, Outlook).
3. Set environment variables with test API endpoints (mock servers).
4. Use **Test this node** on the `Classify spend` prompt for each dataset.
5. Verify each line-item is classified as Productive / Experimental / Shadow IT.
6. Check aggregated totals match the expected figures.
7. Confirm outlier flag fires for datasets containing flagged teams.
8. Run an end-to-end test with Dataset 2 and verify:
   - Teams adaptive card posted to exec channel
   - Outlook PDF sent to CFO/CIO emails
   - SharePoint dashboard list populated with correct rows

### Required Environment Variables

- `spend_CardApiUrl` (point to a mock HTTP endpoint with sample JSON)
- `spend_MonthlyCopilotReportUrl` (point to mock Graph endpoint)
- `spend_OutlierThresholdPerUser` (set to `250` for test — lower than default 500 to catch borderline cases)
- `spend_DashboardListName`
- `spend_ExecChannelId`
- `spend_CfoEmail`
- `spend_CioEmail`

### Mock API Response Template (card API)

```json
{
  "transactions": [
    {"team": "Engineering", "user": 12, "amount": 2520, "month": "2026-09"},
    {"team": "Marketing", "user": 8, "amount": 7120, "month": "2026-09"},
    {"team": "Finance", "user": 4, "amount": 180, "month": "2026-09"},
    {"team": "Growth Lab", "user": 5, "amount": 6000, "month": "2026-09"}
  ]
}
```

### Mock API Response Template (Graph usage)

```json
{
  "reports": [
    {"team": "Engineering", "activeUsers": 12, "totalActions": 89, "month": "2026-09"},
    {"team": "Marketing", "activeUsers": 8, "totalActions": 3, "month": "2026-09"},
    {"team": "Finance", "activeUsers": 4, "totalActions": 12, "month": "2026-09"},
    {"team": "Growth Lab", "activeUsers": 5, "totalActions": 0, "month": "2026-09"}
  ]
}
```
