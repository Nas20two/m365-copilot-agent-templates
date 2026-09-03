# M365 Copilot Studio Workflow Template Library

**Import-ready automation sequences** for Microsoft Copilot Studio — triggers, If/Else, connectors, AI approvals, and human review steps. Pairs with our [existing 7 declarative agent templates](../README.md).

> **Template library design:** See `PLANS/COPILOT_WORKFLOW_TEMPLATE_LIBRARY_DESIGN.md` for the full architecture.

---

## Workflow Catalog

| ID | Workflow | Pairs With | Complexity | Build Order |
|----|----------|------------|------------|-------------|
| 01 | **Document Approval — AI Pre-check + Human Sign-off** | `legal-compliance-agent.yaml` | Advanced | 🥈 Second |
| 02 | **IT Ticket Triage & Escalation** | `it-helpdesk-agent.yaml` | Mid | Third |
| 03 | **HR Onboarding Automation** | `onboarding-buddy-agent.yaml` + `hr-policy-agent.yaml` | Advanced | Fourth |
| 04 | **Email Triage & Daily Digest** | All agents (standalone) | Standard | 🥇 First |
| 05 | **Compliance Document Validation** | `legal-compliance-agent.yaml` | Advanced | Fifth |
| 06 | **AI Spend & Productivity Dashboard** | `agent-cost-intelligence` (nasyhub) | Advanced | Sixth |

---

## What's in Each Workflow

Every workflow ships with 4 deliverables:

1. **YAML spec** — Full Copilot Studio workflow, AgentSchema-aligned, import-ready
2. **Documentation package** — Import steps, connector setup, env variable mapping, permissions, test plan, troubleshooting, DLP governance checklist
3. **Test data** — Sample KB articles, sample documents, sample Forms/SharePoint lists, expected outputs
4. **Setup video script** — Walkthrough video (2–3 min for #1–5 standard/mid complexity workflows; 10–15 min for #6 AI Spend Dashboard with custom connector setup)

---

## Bundles

| Bundle | Contents |
|--------|----------|
| **Starter Pack** | #4 + #5 |
| **Core Three** | #4 + #1 + #2 |
| **Enterprise Workflow Library** | All 5 + future verticals + quarterly updates |
| **AI Spend & Productivity Dashboard** | #6 only — premium/custom connectors |

---

## Agent-Workflow Pairing Map

| Agent Template | Paired Workflow(s) | Cross-sell angle |
|----------------|-------------------|-----------------|
| `legal-compliance-agent.yaml` | #1 Document Approval + #5 Compliance Validation | Ask an agent, execute a workflow |
| `it-helpdesk-agent.yaml` | #2 IT Ticket Triage | Chat → auto-ticket |
| `onboarding-buddy-agent.yaml` | #3 HR Onboarding | Welcome → automated tasks |
| `hr-policy-agent.yaml` | #3 HR Onboarding | Policy answers + benefits Q&A |
| All agents | #4 Email Triage | Inbox-to-agent pipeline |
| `agent-cost-intelligence` | #6 AI Spend Dashboard | AI cost visibility → monthly report |

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
- **Gumroad:** 9 SKUs (6 individual + 3 bundles) — corporate invoice support
- **Microsoft AppSource:** Phase 3+ (gated at $1K MRR)

---

*Built by the MD Copilot Agent team. Part of the [M365 Copilot Agent Templates](../README.md) ecosystem.*
