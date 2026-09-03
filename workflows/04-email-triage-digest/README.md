# Email Triage & Daily Digest — Workflow Template


Quickest path to a shippable Copilot Studio workflow. No premium connectors. Widest buyer pool.

Routes incoming shared-inbox emails through AI classification, surfaces urgent items to Teams + assignee, files attachments to SharePoint, and sends an end-of-day digest.

---

## What It Does

### Trigger
- **New email** to a shared Exchange Online mailbox (event trigger)
- **Scheduled** — daily digest (365-day recurring trigger)

### Logic Flow

```
Email arrives → AI classify priority (Low/Medium/High/Critical)
                     ↓
          ┌─────────────────────┐
          │   If Critical/High  │ → Teams notification + assignee
          │   If Medium         │ → Add to digest only
          │   If Low            │ → File + archive
          └─────────────────────┘
                     ↓
          Summarize long threads (prompt node)
                     ↓
          File attachments to SharePoint library
                     ↓
          End-of-day: digest email to shared inbox with stats
```

### Outputs
- **Teams channel notification** — urgent items with assignee @mention
- **SharePoint library** — filed attachments per email thread
- **Daily digest email** — summary, counts, trends

---

## Requirements

| Item | Detail |
|------|--------|
| License | Copilot Studio (standalone or M365 Copilot) |
| Connectors | Exchange Online, Teams, SharePoint — all **standard** |
| Mailbox | Shared mailbox with Exchange Online license |
| SharePoint | Document library for filed attachments |
| Teams | Channel + webhook for urgent notifications |

---

*Pairs with: any existing MD Copilot Agent (standalone — no specific agent dependency)*
