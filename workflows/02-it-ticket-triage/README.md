# IT Ticket Triage & Escalation — Workflow Template


Automates IT helpdesk ticketing from email, Teams, and agent conversations. LLM classifies requests, creates SharePoint list tickets, manages SLA timers, and escalates aging items.

---

## What It Does

### Triggers
- **Email to helpdesk mailbox** (Exchange Online event)
- **Teams message** (to a monitored channel)
- **Agent conversation** — user messages the IT Helpdesk Agent

### Logic Flow

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

### Key Capabilities
- **LLM classify node** — categorizes requests into standard IT categories
- **SharePoint list ticket** — full CRUD with status workflow
- **SLA timer + escalation** — automatic re-assignment on breach
- **Teams notifications** — per-state-change status updates
- **Weekly summary** — scheduled trigger with stats

---

*Pairs with: `it-helpdesk-agent.yaml`*
