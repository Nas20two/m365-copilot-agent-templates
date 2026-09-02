# M365 Copilot Studio Workflow Template Library

**Import-ready automation sequences** for Microsoft Copilot Studio — triggers, If/Else, connectors, AI approvals, and human review steps. Pairs with our [existing 7 declarative agent templates](../README.md).

> **Template library design:** See `PLANS/COPILOT_WORKFLOW_TEMPLATE_LIBRARY_DESIGN.md` for the full architecture.

---

## Workflow Catalog

| ID | Workflow | Price | Pairs With | Complexity | Build Order |
|----|----------|-------|------------|------------|-------------|
| 01 | **Document Approval — AI Pre-check + Human Sign-off** | $79 | `legal-compliance-agent.yaml` | Advanced | 🥈 Second |
| 02 | **IT Ticket Triage & Escalation** | $49 | `it-helpdesk-agent.yaml` | Mid | Third |
| 03 | **HR Onboarding Automation** | $79 | `onboarding-buddy-agent.yaml` + `hr-policy-agent.yaml` | Advanced | Fourth |
| 04 | **Email Triage & Daily Digest** | $29–$49 | All agents (standalone) | Standard | 🥇 First |
| 05 | **Compliance Document Validation** | $79–$99 | `legal-compliance-agent.yaml` | Advanced | Fifth |

---

## What's in Each Workflow

Every workflow ships with 4 deliverables:

1. **YAML spec** — Full Copilot Studio workflow, AgentSchema-aligned, import-ready
2. **Documentation package** — Import steps, connector setup, env variable mapping, permissions, test plan, troubleshooting, DLP governance checklist
3. **Test data** — Sample KB articles, sample documents, sample Forms/SharePoint lists, expected outputs
4. **Setup video script** — 2–3 min walkthrough

---

## Bundles

| Bundle | Contents | Price |
|--------|----------|-------|
| **Starter Pack** | #4 + #5 | $99 |
| **Core Three** | #4 + #1 + #2 | $179 |
| **Enterprise Workflow Library** | All 5 + future verticals + quarterly updates | $249 |

> ℹ️ Bundle pricing follows VEX's recommendation (see design doc §11). Quarterly updates aligned to Microsoft release waves.

---

## Agent-Workflow Pairing Map

| Agent Template | Paired Workflow(s) | Cross-sell angle |
|----------------|-------------------|-----------------|
| `legal-compliance-agent.yaml` | #1 Document Approval + #5 Compliance Validation | Ask an agent, execute a workflow |
| `it-helpdesk-agent.yaml` | #2 IT Ticket Triage | Chat → auto-ticket |
| `onboarding-buddy-agent.yaml` | #3 HR Onboarding | Welcome → automated tasks |
| `hr-policy-agent.yaml` | #3 HR Onboarding | Policy answers + benefits Q&A |
| All agents | #4 Email Triage | Inbox-to-agent pipeline |

---

## Prerequisites

- **Microsoft Copilot Studio** license (standalone or bundled with M365 Copilot)
- **Power Automate Premium** ($15/user/mo) if using premium connectors — most workflows use standard connectors
- **SharePoint Online** site for knowledge sources and audit logs
- **Exchange Online** mailbox (for email-triggered workflows)
- **Teams** channel for notifications

See individual workflow READMEs for per-workbook requirements.

---

## Distribution

- **GitHub:** [Repo root](../README.md) — free starter workflow (#1), docs, test data
- **Gumroad:** 8 SKUs (5 individual + 3 bundles) — corporate invoice support
- **Microsoft AppSource:** Phase 3+ (gated at $1K MRR)

---

*Built by the MD Copilot Agent team. Part of the [M365 Copilot Agent Templates](../README.md) ecosystem.*
