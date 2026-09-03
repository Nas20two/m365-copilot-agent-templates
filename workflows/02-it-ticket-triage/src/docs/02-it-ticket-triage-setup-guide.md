# IT Ticket Triage & Escalation — Setup Guide


Automates IT helpdesk ticketing from email, Teams, and agent conversations. LLM classifies requests, creates SharePoint list tickets, manages SLA timers, and escalates aging items.

---

## What's Included

| Deliverable | File | Status |
|---|---|---|
| YAML spec | `src/workflow/02-it-ticket-triage-workflow.yaml` | 📝 Atom building |
| Setup guide | This file | ✅ Complete |
| Test data | `src/test-data/it-test-data/` — sample tickets & expected classifications | ✅ Complete |
| Setup video script | `src/video/script.md` | 📝 Coming soon |

---

## Requirements

| Item | Detail |
|---|---|
| License | Copilot Studio (standalone or M365 Copilot) |
| Connectors | SharePoint, Exchange Online, Teams, Outlook — all **standard** |
| Mailbox | Helpdesk shared mailbox with Exchange Online license |
| SharePoint | IT Tickets list with status workflow |
| Teams | Helpdesk channel for ticket + escalation notifications |

---

## Environment Variables

Set these in Copilot Studio after import:

| Variable | Example | Purpose |
|---|---|---|
| `helpdesk_MailboxAddress` | `helpdesk@contoso.com` | Helpdesk mailbox monitored for incoming tickets |
| `helpdesk_TeamsTeamId` | `<TEAMS_TEAM_ID>` | Teams team containing the helpdesk channel |
| `helpdesk_TeamsChannelId` | `<TEAMS_CHANNEL_ID>` | Channel for ticket status notifications + escalation pings |
| `helpdesk_TicketsListName` | `IT Tickets` | SharePoint list where tickets are created/updated |
| `helpdesk_SiteUrl` | `https://contoso.sharepoint.com/sites/IT` | SharePoint site hosting the ticket list |

---

## Connection References

| Connection | Connector | Purpose |
|---|---|---|
| `helpdesk_ExchangeOnlineConnection` | `shared_office365` | Monitor helpdesk mailbox + send escalation emails |
| `helpdesk_SharePointConnection` | `shared_sharepointonline` | Create and update tickets in SharePoint list |
| `helpdesk_TeamsConnection` | `shared_teams` | Post ticket notifications + SLA breach alerts |

---

## Setup (at a glance)

1. **Import YAML** into Copilot Studio (or Power Platform solution)
2. **Configure connection references** — Exchange Online, SharePoint, Teams
3. **Set environment variables** — mailbox, site, channel IDs, ticket list name
4. **Create the SharePoint ticket list** with these columns:
   - `Title` (Single line of text)
   - `RequesterEmail` (Single line of text)
   - `Category` (Choice: Password Reset / Software / Hardware / Access / Other)
   - `Severity` (Choice: P1 Critical / P2 High / P3 Medium / P4 Low)
   - `Status` (Choice: Open / In Progress / Resolved / Closed)
   - `AssignedTo` (Person/Group)
   - `SLADeadline` (Date/Time)
   - `Escalated` (Yes/No)
5. **Load test data** from `src/test-data/it-test-data/` and run validation
6. **Activate** the workflow

---

## Logic Flow

```
Request arrives → LLM classify node (password reset / software / hardware / access)
                      ↓
           ┌─────────────────────────────┐
           │  If/Else: Severity Check    │
           │  P1 Critical → instant Teams ping + assignee  │
           │  P2 High    → ticket + 4h SLA timer             │
           │  P3 Medium  → ticket + 8h SLA timer             │
           │  P4 Low     → ticket + EOD queue                │
           └─────────────────────────────┘
                      ↓
           Create/update ticket in SharePoint list
                      ↓
           SLA timer + escalation loop
           (if SLA breached → notification + re-assign)
                      ↓
           Teams status notification (each state change)
                      ↓
           Weekly summary (scheduled trigger) to helpdesk channel
```

---

## Test Plan

1. **Unit: LLM classify** — Feed each sample ticket. Verify category output matches expected.
2. **Unit: Severity condition** — Trace each severity P1–P4. Confirm correct action path and SLA timer.
3. **Integration: End-to-end** — Send a P1 email to helpdesk mailbox. Confirm: ticket created, Teams ping sent, SLA timer started.
4. **Regression: SLA breach** — Let a P2 ticket age past 4h. Confirm escalation fires.
5. **Regression: Weekly summary** — Manually trigger scheduled digest. Confirm formatting.

---

## Troubleshooting

| Symptom | Likely Cause | Fix |
|---|---|---|
| Email not triggering flow | Mailbox not connected or filter too strict | Verify `helpdesk_MailboxAddress` and test with matching email |
| Classification always returns "Other" | Prompt node not receiving full body | Check dynamic values in classify prompt |
| SLA timers not firing | Recurrence misconfigured | Confirm start time and timezone |
| Teams notification missing | Teams connector not authorized | Re-authenticate `helpdesk_TeamsConnection` |
| SharePoint write fails | Column names mismatch | Ensure ticket list column names match exactly |

---

## Pricing Rationale

$49 positions it as the mid-tier workflow — more complex than Email Triage ($29–$49) but simpler than Document Approval ($79). Justified by SLA timer + escalation loop (a premium automation pattern), multi-channel triggers, and the weekly summary deliverable.

*Pairs with: `it-helpdesk-agent.yaml`*
