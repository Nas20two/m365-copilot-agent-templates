# Compliance Document Validation — Workflow Template


Validates documents against regulatory and policy guidelines. Categorizes violations by risk level, routes to human legal review, and maintains a complete audit trail.

---

## What It Does

### Triggers
- **Document uploaded** to compliance SharePoint library (event)
- **Agent conversation** — user messages Legal & Compliance Advisor

### Logic Flow

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

### Compliance Features
- EU AI Act-ready governance checklist
- DLP-first design (no data exfiltration)
- Full audit log (who reviewed, what changed, final decision)
- Human oversight stages with RFI fallback

---

*Pairs with: `legal-compliance-agent.yaml`*

Premium price justified by governance value — enterprise buyers pay premiums for audit-ready compliance automation.
