# M365 Copilot Studio Workflow Template Library

**Import-ready automation sequences** for Microsoft Copilot Studio — triggers, If/Else, connectors, AI approvals, and human review steps. Pairs with our [existing 7 declarative agent templates](../README.md).

---

## Workflow Catalog

| # | Workflow | Price | Pairs With | Complexity |
|---|----------|-------|-----------|------------|
| 1 | **Document Approval — AI Pre-check + Human Sign-off** | $79 | `legal-compliance-agent.yaml` | Advanced |
| 2 | **IT Ticket Triage & Escalation** | $49 | `it-helpdesk-agent.yaml` | Mid |
| 3 | **HR Onboarding Automation** | $79 | `onboarding-buddy-agent.yaml` + `hr-policy-agent.yaml` | Advanced |
| 4 | **Email Triage & Daily Digest** | $29–$49 | All agents (standalone) | Standard |
| 5 | **Compliance Document Validation** | $79–$99 | `legal-compliance-agent.yaml` | Advanced |

---

## What's in Each Workflow

Every workflow ships with 4 deliverables:

1. **YAML spec** — Full Copilot Studio workflow, AgentSchema-aligned, import-ready
2. **Documentation package** — Import steps, connector setup, env variable mapping, permissions, test plan, troubleshooting, DLP governance checklist
3. **Test data** — Sample KB articles, sample documents (invoice, contract, expense), sample Forms/SharePoint lists, expected outputs
4. **Setup video script** — 2–3 min walkthrough

---

## Bundles (coming soon)

| Bundle | Contents | Price |
|--------|----------|-------|
| **Workflow Starter Pack** | #4 + #5 | $129 |
| **Enterprise Workflow Library** | All 5 + future verticals | $249–$297 |

Includes quarterly updates aligned to Microsoft release waves.

---

## Prerequisites

- **Microsoft Copilot Studio** license (standalone or bundled with M365 Copilot)
- **Power Automate Premium** ($15/user/mo) if using premium connectors — most workflows designed for standard connectors
- **SharePoint Online** site for knowledge sources and audit logs
- **Exchange Online** mailbox (for email-triggered workflows)

See individual workflow READMEs for per-workbook requirements.

---

## Distribution

- **GitHub:** [Repo root](../README.md) — free starter workflow, docs, test data
- **Gumroad:** Paid templates with corporate invoice support
- **Microsoft AppSource:** (planned) — enterprise discovery

---

*Built by the MD Copilot Agent team. Part of the [M365 Copilot Agent Templates](../README.md) ecosystem.*
