# AI Spend & Productivity Dashboard — Setup Guide


Monthly AI spend intelligence for execs. Pulls card transactions and M365 Copilot usage data, classifies every dollar as productive / experimental / shadow IT, flags outlier teams, and delivers a CFO-ready report.

---

## What's Included

| Deliverable | File | Status |
|---|---|---|
| YAML spec | `src/workflow/06-ai-spend-dashboard-workflow.yaml` | 📝 Atom building |
| Setup guide | This file | ✅ Complete |
| Test data | `src/test-data/spend-test-data/` — sample transactions & expected classifications | ✅ Complete |
| Setup video script | `src/video/script.md` | 📝 Coming soon |

---

## Requirements

| Item | Detail |
|---|---|
| License | Copilot Studio (standalone or M365 Copilot) |
| Connectors | HTTP, SharePoint, Teams, Outlook — all **standard** |
| API access | Corporate card API + M365 Graph usage reports |
| SharePoint | Spend dashboard list (Power BI source) |
| Teams | Exec channel for adaptive card delivery |
| Optional | Power Automate Premium ($15/user/mo) for Concur/Expensify premium connectors |

---

## Environment Variables

Set these in Copilot Studio after import:

| Variable | Example | Purpose |
|---|---|---|
| `spend_CardApiUrl` | `https://api.corpcard.com/v1/transactions` | Corporate card API for transaction data |
| `spend_MonthlyCopilotReportUrl` | `https://graph.microsoft.com/v1.0/reports/monthly/copilotUsage` | M365 Graph endpoint for Copilot usage data |
| `spend_OutlierThresholdPerUser` | `500` | Spend per user (USD) above which a team is flagged |
| `spend_DashboardListName` | `AI Spend Dashboard` | SharePoint list for dashboard (Power BI source) |
| `spend_ExecChannelId` | `<TEAMS_CHANNEL_ID>` | Teams channel for executive summary adaptive cards |
| `spend_CfoEmail` | `cfo@contoso.com` | Email for monthly PDF report |
| `spend_CioEmail` | `cio@contoso.com` | CC email for monthly PDF report |

---

## Connection References

| Connection | Connector | Purpose |
|---|---|---|
| `spend_HttpConnection` | `shared_http` | Call corporate card API + M365 Graph |
| `spend_SharePointConnection` | `shared_sharepointonline` | Write to spend dashboard list |
| `spend_TeamsConnection` | `shared_teams` | Post adaptive card to exec channel |
| `spend_OutlookConnection` | `shared_office365` | Send monthly PDF report |

---

## Setup (at a glance)

1. **Import YAML** into Copilot Studio
2. **Configure connection references** — HTTP, SharePoint, Teams, Outlook
3. **Set environment variables** — API URLs, threshold, dashboard list name, exec channel, emails
4. **Create SharePoint list** (`AI Spend Dashboard`) with columns:
   - `Month` (Date/Time)
   - `TeamName` (Single line)
   - `Department` (Single line)
   - `TotalSpend` (Currency)
   - `ProductiveSpend` (Currency)
   - `ExperimentalSpend` (Currency)
   - `ShadowITSpend` (Currency)
   - `UsersOnPlan` (Number)
   - `OutlierFlagged` (Yes/No)
   - `Narrative` (Multiple lines)
5. **Configure API access** — Corporate card API key + M365 Graph delegated permissions
6. **Load test data** from `src/test-data/spend-test-data/` and run validation
7. **Activate** the workflow (scheduled — 1st of month at 9am)

---

## Logic Flow

```
Monthly trigger → HTTP (card API) + HTTP (Graph API usage reports)
                      ↓
           ┌─────────────────────────────┐
           │  Condition: Standard conns   │
           │  sufficient?                 │
           │  Yes → HTTP proceed          │
           │  No  → Flag premium needed   │
           └─────────────────────────────┘
                      ↓
           AI Classify: Productivity / Experimental / Shadow IT
                      ↓
           Aggregate: $/agent, $/team, $/user, $/task
                      ↓
           ┌─────────────────────────────┐
           │  If/Else: Outlier team?      │
           │  Spending > $X/user w/ no    │
           │  measurable output → flag     │
           └─────────────────────────────┘
                      ↓
           AI executive summary + trend commentary
                      ↓
           RFI to flagged team leads
                      ↓
           SharePoint list (Power BI source)
                      ↓
           Teams adaptive card + Outlook PDF to CFO/CIO
```

---

## Test Plan

1. **Unit: HTTP connectors** — Test with sample API responses to verify data ingestion.
2. **Unit: AI classify** — Feed sample transactions. Verify each correctly classified as Productive / Experimental / Shadow IT.
3. **Unit: Outlier detection** — Set low threshold, include a team with high per-user spend but no output. Verify flag fires.
4. **Integration: End-to-end** — Run the workflow with test data. Confirm: SharePoint list populated, Teams card posted, Outlook PDF sent.
5. **Regression: Partial data** — Simulate missing usage report. Confirm graceful handling and fallback narrative.

---

## Premium Connector Note

Concur, Expensify, and other expense-system connectors are premium (require Power Automate Premium $15/user/mo). This workflow ships with **HTTP connector (standard)** + manual CSV export instructions as the default path. Premium connector integration is documented as an upgrade for enterprise buyers.

---

## Troubleshooting

| Symptom | Likely Cause | Fix |
|---|---|---|
| API call fails | API key not configured or endpoint changed | Verify `spend_CardApiUrl` and authentication method |
| Classification all "Productive" | Threshold not strict enough | Adjust the AI classify prompt with more explicit Shadow IT patterns |
| Outlier flags not firing | Threshold too high for your data | Lower `spend_OutlierThresholdPerUser` |
| SharePoint list empty | List name mismatch or write permission missing | Confirm `spend_DashboardListName` and reauthenticate SharePoint connection |
| PDF not sending | Outlook connection not authorized | Re-authenticate `spend_OutlookConnection` |

---

## Pricing Rationale

$99 is the premium tier — justified by multi-source data ingestion (card API + Graph), AI classification with three output categories, outlier detection logic, and dual-channel executive delivery (Teams card + Outlook PDF). Targets CFO/CIO buyers who manage six-figure AI budgets.

*Pairs with: `agent-cost-intelligence` (nasyhub.com)*
