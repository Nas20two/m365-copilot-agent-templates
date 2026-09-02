# Compliance Document Validation — Setup Guide

> **Price:** $79–$99 · **Build time:** ~10–14 hours · **Difficulty:** Advanced

Validates documents against regulatory and policy guidelines. Categorizes violations by risk level, routes to human legal review, and maintains a complete audit trail.

---

## What's Included

| Deliverable | File | Status |
|---|---|---|
| YAML spec | `src/workflow/05-compliance-validation-workflow.yaml` | 📝 Atom building |
| Setup guide | This file | ✅ Complete |
| Test data | `src/test-data/compliance-test-data/` — sample documents & expected validation results | ✅ Complete |
| Setup video script | `src/video/script.md` | 📝 Coming soon |

---

## Requirements

| Item | Detail |
|---|---|
| License | Copilot Studio + M365 Copilot (for agent trigger) |
| Connectors | SharePoint, Exchange Online, Teams, Outlook — all **standard** |
| AI feature | AI approvals (Copilot Studio workflows) — validates against policy criteria |
| SharePoint | Document library + compliance audit list |
| Teams | Legal review channel for violation alerts |
| Mailbox | Legal reviewer mailbox for urgent notifications |

---

## Environment Variables

Set these in Copilot Studio after import:

| Variable | Example | Purpose |
|---|---|---|
| `compliance_LibraryUrl` | `https://contoso.sharepoint.com/sites/Compliance/Documents` | SharePoint document library monitored for uploads |
| `compliance_AuditListName` | `Compliance Validation Log` | SharePoint list for full audit trail |
| `compliance_LegalReviewerEmail` | `legal@contoso.com` | Email notified for high/medium-risk violations |
| `compliance_RiskThreshold` | `50` | Risk score threshold (0–100) above which human review is required |

---

## Connection References

| Connection | Connector | Purpose |
|---|---|---|
| `compliance_SharePointConnection` | `shared_sharepointonline` | Monitor document library, write audit log, file reports |
| `compliance_ExchangeOnlineConnection` | `shared_office365` | Notify legal reviewer on violation detection |
| `compliance_TeamsConnection` | `shared_teams` | Post violation alerts to legal review channel |

---

## Setup (at a glance)

1. **Import YAML** into Copilot Studio
2. **Configure connection references** — SharePoint, Exchange Online, Teams
3. **Set environment variables** — document library URL, audit list name, reviewer email, risk threshold
4. **Create SharePoint assets:**
   - Document library for compliance uploads
   - `Compliance Validation Log` list with columns: DocumentName, RiskScore, ViolationType, Status (Pending / Under Review / Resolved), Reviewer, Decision, Notes
5. **Define policy criteria** — configure the validation prompt node with your regulatory requirements (GDPR, SOC 2, HIPAA, internal policy)
6. **Load test data** from `src/test-data/compliance-test-data/` and run validation
7. **Activate** the workflow

---

## Logic Flow

```
Document uploaded → Extract applicable guidelines/policies
                      ↓
           Validate document against criteria
                      ↓
           ┌────────────────────────────┐
           │  If/Else: Violation Risk   │
           │  High risk → Human legal review (urgent)  │
           │  Medium → Human legal review (standard)   │
           │  Low/None → Auto-approve                  │
           └────────────────────────────┘
                      ↓
           Remediation task created (for violations)
                      ↓
           Audit trail → SharePoint (full chain)
                      ↓
           Approved/flagged report to library
```

---

## Test Plan

1. **Unit: Document classification** — Upload each sample document. Verify risk score and violation type match expected values.
2. **Unit: Risk branching** — For high-risk input: confirm urgent Teams + email. For low-risk: confirm auto-approve path.
3. **Integration: End-to-end** — Upload a document with known PII exposure. Trace through validation → risk classification → legal review → remediation task.
4. **Regression: Audit log** — After any validation run, confirm the Compliance Validation Log has a complete entry with all fields populated.
5. **Regression: Multi-document** — Upload 3 documents in sequence. Verify each creates an independent audit trail entry.

---

## Troubleshooting

| Symptom | Likely Cause | Fix |
|---|---|---|
| Document upload not triggering workflow | Library trigger filter too specific or library wrong URL | Verify `compliance_LibraryUrl` points to the exact document library |
| Risk score always 0 | Validation prompt not receiving document content | Check the dynamic content reference in the "Extract guidelines" prompt node |
| All documents auto-approved | Risk threshold too high | Lower `compliance_RiskThreshold` env var |
| Audit log entry missing | SharePoint list column mismatch | Confirm Compliance Validation Log column names match workflow schema |
| Teams alert not posted | Teams connection not configured for the legal review channel | Re-authenticate `compliance_TeamsConnection` and verify channel ID |

---

## Pricing Rationale

$79–$99 premium positioning justified by enterprise governance value — EU AI Act readiness, DLP-first architecture, and full audit trail covering who reviewed what and when. Enterprise buyers pay premiums for compliance automation that reduces audit prep cost.

*Pairs with: `legal-compliance-agent.yaml`*
