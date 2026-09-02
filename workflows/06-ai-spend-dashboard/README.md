# AI Spend & Productivity Dashboard — Workflow Template

> **Price:** $99 · **Build time:** ~10–14 hours · **Difficulty:** Advanced

Monthly AI spend intelligence for execs. Pulls card transactions and M365 Copilot usage data, classifies every dollar as productive / experimental / shadow IT, flags outlier teams, and delivers a CFO-ready report.

---

## What It Does

### Triggers
- **Scheduled** — monthly (1st of month at 9am)
- **Manual** — on-demand for demos or executive requests

### Logic Flow

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
               │  If/Else: Outlier team?       │
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

### Key Capabilities
- **HTTP connector (standard)** — pulls from corporate card API + M365 Graph usage reports
- **AI classify node** — categorizes spend lines (Productivity / Experimental / Shadow IT)
- **Aggregate variables** — $ per agent, per team, per user, per task
- **Outlier detection** — teams spending above threshold with no measurable output
- **Executive report** — AI-generated narrative with trend commentary
- **Multi-channel delivery** — Teams adaptive card + Outlook PDF summary
- **Power BI source** — writes to SharePoint list for dashboard tooling

---

## Premium Connector Note

Concur, Expensify, and other expense-system connectors are premium (require Power Automate Premium $15/user/mo). This workflow ships with **HTTP connector (standard)** + manual CSV export instructions as the default path. Premium connector integration is documented as an upgrade for enterprise buyers.

---

## Requirements

| Item | Detail |
|------|--------|
| License | Copilot Studio (standalone or M365 Copilot) |
| Connectors | HTTP, SharePoint, Teams, Outlook — all **standard** |
| API access | Corporate card API + M365 Graph usage reports |
| SharePoint | Spend dashboard list (Power BI source) |
| Teams | Exec channel for adaptive card |

---

*Pairs with: `agent-cost-intelligence` (nasyhub.com)*
