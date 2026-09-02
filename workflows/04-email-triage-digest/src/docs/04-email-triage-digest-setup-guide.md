# Email Triage & Daily Digest — Workflow Template

> **Price:** $29–$49 · **Build time:** ~4–6 hours · **Difficulty:** Standard

Quickest path to a shippable Copilot Studio workflow. No premium connectors. Widest buyer pool.

---

## What It Does

Routes incoming shared-inbox emails through AI classification, surfaces urgent items to Teams + assignee, files attachments to SharePoint, and sends an end-of-day digest.

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
- Teams channel notification (urgent items with assignee @mention)
- SharePoint library with filed attachments per email thread
- Daily digest email: summary, counts, trends

---

## What's Included

| Deliverable | File | Status |
|---|---|---|
| YAML spec | `04-email-triage-digest-workflow.yaml` | ✅ Ready for review |
| Documentation package | `IMPORT_GUIDE.md` | 📝 Drafting |
| Test data | `test-data/` sample emails & expected classifications | 📝 Drafting |
| Setup video script | `SETUP_VIDEO_SCRIPT.md` | 📝 Drafting |

---

## Requirements

| Item | Detail |
|------|--------|
| License | Copilot Studio (standalone or M365 Copilot) |
| Connectors | Exchange Online, Teams, SharePoint — all **standard** (no premium needed) |
| Mailbox | Shared mailbox with Exchange Online license |
| SharePoint | Document library for filed attachments |
| Teams | Channel + webhook for urgent notifications |

---

## Setup (at a glance)

1. Import the YAML into Copilot Studio (or Power Platform solution)
2. Configure connection references: mailbox, SharePoint site, Teams webhook
3. Set environment variables (classification prompt, urgency thresholds, digest time)
4. Test with sample emails from `test-data/`
5. Activate

Full steps in `IMPORT_GUIDE.md`.

---

## Pricing Rationale

Loss leader / entry tier. Standard connectors only means no extra licensing friction for buyers. $29 single, $49 with test data + setup video and priority support.

*Pairs with: any existing MD Copilot Agent (standalone — no specific agent dependency)*
