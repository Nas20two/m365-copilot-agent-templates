# Document Approval — AI Pre-check + Human Sign-off


Flagship enterprise workflow. Automates document review — invoices, POs, contracts, expense reports — by extracting key fields, validating against policy thresholds, and routing to the right approval path (AI or human) with full audit trail.

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
- **AI classification node** — identifies document type, extracts vendor/amount/date
- **Policy If/Else** — configurable threshold rules (approve under $500, flag over $5,000)
- **AI approvals** — auto-decide on routine items within policy
- **Human RFI** — Request for Information for policy exceptions or ambiguous documents
- **Teams adaptive card** — rich preview with approve/reject buttons
- **Outlook notification** — email to approver with direct link
- **Audit log** — full chain to SharePoint list

---

## Variants

| Variant | Policy Threshold | Best for |
|---------|-----------------|----------|
| **Expense Reports** | Auto-approve < $500, flag > $5,000 | Finance teams |
| **Purchase Orders** | Auto-approve < $2,500, flag > $25,000 | Procurement |
| **Invoices** | Auto-match PO, flag discrepancies | AP teams |
| **Contracts** | All human review (no auto-approve) | Legal team |

---

## Requirements

| Item | Detail |
|------|--------|
| License | Copilot Studio + M365 Copilot |
| Connectors | SharePoint, Exchange Online, Teams, Outlook — all **standard** |
| AI feature | AI approvals + RFI |
| SharePoint | Document library + audit log list |
| Teams | Channel for adaptive card notifications |

---

*Pairs with: `legal-compliance-agent.yaml`*
