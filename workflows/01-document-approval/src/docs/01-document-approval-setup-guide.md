# Document Approval — AI Pre-check + Human Sign-off

> **Price:** $79 · **Build time:** ~8–12 hours · **Difficulty:** Advanced

**Flagship enterprise workflow.** Automates document review — invoices, POs, contracts, expense reports — by extracting key fields, validating against policy thresholds, and routing to the right approval path (AI or human) with full audit trail.

---

## What It Does

### Triggers
- **Email attachment** received (invoice, PO, contract, expense report)
- **SharePoint file created** in a monitored document library
- **Agent conversation** — user initiates via an MD Copilot Agent (e.g. Legal & Compliance Advisor)

### Logic Flow

```
Document arrives → AI classify & extract (vendor, amount, date, doc type)
                          ↓
               ┌──────────────────────────┐
               │  If/Else: Policy Check   │
               │  Under threshold → AI approve  │
               │  Over threshold  → Human review │
               │  Policy exception  → Human RFI  │
               └──────────────────────────┘
                          ↓
               AI Approval stage (auto-decide on routine items)
                          ↓
               Human RFI (Request for Information) for exceptions
                          ↓
               Teams adaptive card + Outlook notification
                          ↓
               Audit log to SharePoint list
```

### Key Capabilities
- **AI classification node** — identifies document type, extracts vendor/amount/date using Copilot Studio's prompt node
- **Policy If/Else** — configurable threshold rules (e.g. "approve expenses under $500, flag over $5,000")
- **AI approvals** — auto-decide on routine items within policy
- **Human RFI** — Request for Information step for policy exceptions or ambiguous documents
- **Teams adaptive card** — rich preview with approve/reject buttons
- **Outlook notification** — email to approver with direct link
- **Audit log** — full chain to SharePoint list (who, what, when, outcome)

---

## What's Included

| Deliverable | File | Status |
|---|---|---|
| YAML spec | `01-document-approval-workflow.yaml` | ✅ Ready for review |
| Documentation package | `IMPORT_GUIDE.md` | 📝 Drafting |
| Test data | `test-data/` — sample invoices, POs, expense reports with expected classifications | 📝 Drafting |
| Setup video script | `SETUP_VIDEO_SCRIPT.md` | 📝 Drafting |

---

## Requirements

| Item | Detail |
|------|--------|
| License | Copilot Studio + M365 Copilot (for agent conversation trigger variant) |
| Connectors | SharePoint, Exchange Online, Teams, Outlook — all **standard** |
| AI feature | AI approvals (Copilot Studio workflows) + RFI (Request for Information) |
| SharePoint | Document library + audit log list |
| Teams | Channel for adaptive card notifications |

---

## Variants

This workflow ships with configurable policy presets:

| Variant | Policy Threshold | Best for |
|---------|-----------------|----------|
| **Expense Reports** | Auto-approve < $500, flag > $5,000 | Finance teams |
| **Purchase Orders** | Auto-approve < $2,500, flag > $25,000 | Procurement |
| **Invoices** | Auto-match PO, flag discrepancies | AP teams |
| **Contracts** | All human review (no auto-approve) | Legal team |

Switch presets by changing environment variables — no YAML editing.

---

## Setup (at a glance)

1. Import YAML into Copilot Studio
2. Configure connection references (SharePoint lists, mailbox, Teams)
3. Set policy threshold vars (`APPROVAL_THRESHOLD_LOW`, `APPROVAL_THRESHOLD_HIGH`, `DOC_TYPE`)
4. Load test data from `test-data/` and run validation
5. Activate workflow

Full steps in `IMPORT_GUIDE.md`.

---

## Pricing Rationale

$79 positions it as the anchor — below Kesslernity's $97 agent kit per-workflow average, above the Etsy/CodeCanyon floor. Justified by three premium features: AI + human review chain, SharePoint audit trail, and multimodal triggers (email, SharePoint, agent conversation).

*Pairs with: `legal-compliance-agent.yaml`*
