# AI Spend & Productivity Dashboard — v2 Blueprint

**Date:** 2026-09-03
**Author:** Kai (CTO) — based on discussion with NaSy for IAG (Jon + Raj) pitch
**Repo:** `Nas20two/m365-copilot-agent-templates`
**Status:** 🟡 Design — not yet built

---

## Executive Summary

This document captures the v2 design for the AI Spend & Productivity Dashboard workflow template, based on the IAG pitch discussion. The v1 template is a Copilot Studio workflow that pulls card transactions + M365 Graph usage data, classifies spend, and outputs a Teams adaptive card + Outlook PDF. 

**v2 adds:** Approval gate architecture, build time estimates, Power BI dashboard integration, Vela cross-reference, and client deployment playbook.

---

## 1. Architecture: How It Works

### Data Sources

| Source | Access | Difficulty | Phase |
|--------|--------|------------|-------|
| **M365 Graph usage reports** | `GET /reports/getM365CopilotUserDetail` — single HTTP call | 🟡 Moderate (IT needs to grant app permission, 1-2 days) | Phase 1 |
| **Corporate card / expense API** | Concur, Expensify, Netsuite, Coupa — requires admin access + paid tier | 🔴 Hard (Finance approval, 3-7 days) | Phase 2 (or CSV workaround) |
| **Manual CSV upload** | Finance exports and uploads monthly | 🟢 Easy (no API access needed) | Fallback |

### Data Flow

```
M365 Graph API ─┐
                ├──→ SharePoint List (spend records)
Corporate Card ─┘          │
                           ├──→ Power BI Dashboard (exec visuals)
                           ├──→ Teams Adaptive Card (monthly digest)
                           └──→ Outlook PDF (CFO/CIO report)
```

### Outputs

| Output | Audience | Format | Status |
|--------|----------|--------|--------|
| Teams adaptive card | All staff | "Team X spent $Y — 40% experimental" | ✅ v1 built |
| Outlook PDF | CFO/CIO | Monthly summary with trend commentary | ✅ v1 built |
| Power BI dashboard | Execs, Finance | Interactive — charts, filters, drill-down | ⏳ v2 not built |
| RFI to team leads | Team leads | "Justify your spend" with approve/reject | ✅ v1 built |

---

## 2. Build Time Estimates

### One-Time Template Build (v1 — already done)

| Component | Time |
|-----------|------|
| Workflow YAML (triggers, logic, AI classify, aggregation, outlier detection, delivery) | 10-14 hrs |
| Documentation (setup guide, test data, video script) | Included in above |
| **Total v1** | **10-14 hrs** |

### v2 Additions (not yet built)

| Component | Time | Buzz Agent |
|-----------|------|------------|
| Power BI report (.pbix) — 3 pages (Overview, Teams, Trends) | 2-3 hrs | Atom (dev) |
| SharePoint list schema design | 1 hr | SATORI |
| Power BI visual research (what works for execs) | 1 hr | VEX |
| Dashboard critique (is it answering the right questions?) | 30 min | THORN |
| Test with real data shape | 30 min | Fizz |
| Client deployment documentation | 1 hr | Honey |
| **Total v2** | **~6-8 hrs** | **Buzz squad (parallel)** |

### Per-Client Deployment

| Step | Time | Dependency |
|------|------|------------|
| Import workflow YAML into their Copilot Studio | 5 min | None |
| Import SharePoint list template | 5 min | None |
| Open Power BI report, re-point data source | 10 min | None |
| Wire M365 Graph API permissions | 1-2 days | Their IT admin |
| Wire corporate card API (if Phase 2) | 3-7 days | Their Finance + IT |
| Connect their Teams/SharePoint channels | 30 min | None |
| **Total per-client (technical)** | **~2-4 hrs** | API access is the bottleneck |

---

## 3. Approval Gates

### Gate 1: Phase 1 vs Phase 2 (Client Decision)

| | Phase 1 (MVP) | Phase 2 (Full) |
|---|---|---|
| **Data** | M365 Graph only | Card API + M365 Graph |
| **API access** | IT ticket only | IT + Finance approval |
| **Time to live** | 1-2 days | 1-2 weeks |
| **Value** | Agent usage per user/team/app | Full spend picture |
| **Recommendation** | ✅ Start here | 🟡 Upgrade path |

### Gate 2: Approval Workflow (Built into Template)

The workflow has built-in approval gates:

| Gate | What Happens | Who |
|------|-------------|-----|
| **Spend gate** | If team spend > $X/user with no measurable output → flag | System |
| **RFI gate** | Flagged team lead gets a Teams card: "Justify this spend" | Team Lead |
| **Escalation gate** | If no response in 3 days → escalate to exec | Manager |
| **Publish gate** | All changes staged until human approves | Finance/Exec |

### Gate 3: Deployment Approval (Per Client)

| Step | Approver | Time |
|------|----------|------|
| 1. Graph API permission granted | Their IT admin | 1-2 days |
| 2. SharePoint list created | Their IT or us | 5 min |
| 3. Workflow imported | Us | 5 min |
| 4. Power BI report deployed | Us | 10 min |
| 5. Test run with their data | Both | 30 min |
| 6. Executive sign-off | Their CFO/CIO | Variable |

---

## 4. The Power BI Dashboard (v2 — Not Yet Built)

### Page 1: Executive Overview

```
┌──────────────────────────────────────────────────┐
│ AI Spend Overview — August 2026                    │
│ Total Spend: $24,500    Target: $20,000    +22.5%   │
│                                                    │
│ ┌─────────────┐  ┌─────────────┐  ┌─────────────┐ │
│ │ By Category │  │ By Team     │  │ Trend       │ │
│ │ (Pie)       │  │ (Bar)       │  │ (Line)      │ │
│ │             │  │             │  │             │ │
│ │ Prod  45%   │  │ Eng    $8K  │  │ Jul ████    │ │
│ │ Exp   35%   │  │ Sales  $6K  │  │ Aug ██████  │ │
│ │ Shadow 20%  │  │ Mktg  $5K  │  │ Sep ████    │ │
│ └─────────────┘  └─────────────┘  └─────────────┘ │
│                                                    │
│ Top 3 Outliers:                                    │
│ 🚨 Engineering: $8K (+$2K vs target)               │
│ 🟡 Sales Ops: $2K on experimental tools            │
│ ✅ HR: $500 — under budget                          │
└──────────────────────────────────────────────────┘
```

### Page 2: Team Deep-Dive

- Drill-down by team
- Per-user spend breakdown
- Tool/app categorization
- Month-over-month comparison
- Action items (auto-flagged)

### Page 3: Recommendations

- "Phase out: Tool X — $3K/mo with 0 measurable output"
- "Consolidate: Tool Y + Tool Z overlap"
- "Renegotiate: Tool A contract expires next month"

### Build Time: 2-3 hrs (Atom agent)

---

## 5. Vela Integration

### What is Vela?

**Vela** is a standalone web app at **https://nasyhub.com/vela** — an AI cost intelligence tool that:
- Audits AI spend across ANY LLM/provider (OpenAI, Anthropic, Google, open-source)
- Works with any agent platform (not just M365)
- Gives a free report in 60 seconds — no signup, no API keys
- Runs in a browser — no deployment, no infrastructure

### How They Work Together

| | Vela (Web App) | This Workflow (Copilot Studio) |
|---|---|---|
| **Scope** | Any AI spend (any provider) | Microsoft M365 only |
| **Audience** | Any company | Microsoft shops (IAG, enterprise) |
| **Setup** | Browser, 60 seconds | Copilot Studio + SharePoint + API |
| **Output** | Free online report | Teams card + PDF + Power BI |
| **Data** | User-submitted (API keys, usage data) | Corporate card + M365 Graph |
| **Cost** | Free (for now) | Included in Copilot Studio license |

### Standalone or Together?

| Scenario | Use |
|----------|-----|
| **Vela alone** | Quick audit, broad view across all AI spend, any company |
| **Workflow alone** | Deep M365-specific view, recurring monthly, inside Teams |
| **Both together** | 🔥 Best for IAG pitch. Vela gives the broad picture (all AI spend, all providers). The workflow gives the deep M365 drill-down (per-user, per-team, per-app). Cross-reference: "Vela shows 40% waste overall. The workflow shows it's Engineering's experimental tools." |

### For the IAG Pitch

- Lead with **Vela** as the free, fast, broad audit — "see what we can do in 60 seconds"
- Layer the **workflow** as the deep, recurring, M365-specific engine
- The Power BI dashboard is the **exec face** — the thing Jon shows Raj's boss
- Vela URL: **https://nasyhub.com/vela**

---

## 6. Client Deployment Playbook

### For a New Client (e.g. IAG Phase 1)

**Step 1: IT Permission (1-2 days)**
- Their IT admin grants Graph API permission
- We provide the exact permission scope in a single doc

**Step 2: Import (15 min)**
- Import workflow YAML into their Copilot Studio
- Import SharePoint list template
- We do this in a screenshare or send files

**Step 3: Configure (30 min)**
- Connect their Teams channel
- Point workflow to their SharePoint list
- Set up the monthly schedule

**Step 4: Power BI (10 min)**
- Open the .pbix file
- Re-point data source to their SharePoint list
- Publish to their Power BI Service

**Step 5: Test (30 min)**
- Run a manual trigger
- Verify Teams card appears
- Verify SharePoint list populates
- Verify Power BI reflects data

**Step 6: Go Live**
- Schedule the monthly trigger
- Send the first PDF to CFO/CIO
- Demo the Power BI dashboard

### Deployment Checklist

- [ ] Graph API app permission granted
- [ ] Workflow YAML imported
- [ ] SharePoint list created
- [ ] Teams channel connected
- [ ] Monthly schedule set
- [ ] Power BI .pbix deployed
- [ ] Test run completed
- [ ] First PDF sent to execs
- [ ] Dashboard shared with stakeholders

---

## 7. What NOT to Build (v2 Scope)

| Don't | Why |
|-------|-----|
| ❌ Build a custom billing system | Use Stripe/Gumroad |
| ❌ Build a custom expense integration | Use the CSV fallback; upgrade to API when client has it |
| ❌ Build a mobile app | Teams mobile + Power BI mobile covers this |
| ❌ Build a real-time dashboard | Monthly is fine for execs; real-time adds complexity |
| ❌ Build for non-Microsoft shops | This workflow is M365-only. Vela covers everyone else. |

---

## 8. Stale Reference Fix

The v1 template says:

> _Pairs with: `agent-cost-intelligence` (nasyhub.com)_

This should be updated to:

> _Pairs with: **Vela** (https://nasyhub.com/vela) — NaSy Hub's AI cost intelligence web app. Vela audits any LLM/provider in 60 seconds. This workflow gives the deep M365 drill-down. Together: broad picture + deep detail._

---

*This is a design document, not a build ticket. When NaSy says "build it," the Buzz agents are briefed and ready to execute in ~6-8 hrs.*