# M365 Copilot Agents — Corporate Use Case Templates (YAML)

**Source:** MD Knowledge Assistant export (MedicalDirector, Aug 31 2026)
**Format:** Copilot Studio CLI Agent (`cliagent-1.0.0`) — declarative agents deployable via YAML solution packages
**Stack:** M365 Copilot + SharePoint + Power Platform

## How to Use

1. Copy the `templates/` YAML for your use case
2. Replace placeholders: `<COMPANY_NAME>`, `<SHAREPOINT_SITE_URL>`, model choice
3. Edit the `instructions` section for your org's tone and rules
4. Import via Copilot Studio or Power Platform CLI

## Use Case Index

| # | Agent | Team | YAML | Build Time |
|---|-------|------|------|------------|
| 1 | **CS Knowledge Assistant** | Customer Success | `cs-knowledge-agent.yaml` | ~4-6 hrs |
| 2 | **Sales Enablement** | Sales | `sales-enablement-agent.yaml` | ~4-6 hrs |
| 3 | **IT Help Desk** | IT / Service Desk | `it-helpdesk-agent.yaml` | ~4-6 hrs |
| 4 | **HR Policy Assistant** | HR / People Ops | `hr-policy-agent.yaml` | ~3-5 hrs |
| 5 | **New Hire Onboarding** | All | `onboarding-buddy-agent.yaml` | ~3-5 hrs |
| 6 | **Project Knowledge** | PMO / Engineering | `project-knowledge-agent.yaml` | ~4-6 hrs |
| 7 | **Legal & Compliance** | Legal / Compliance | `legal-compliance-agent.yaml` | ~5-8 hrs |

## Workflow Templates

**Turn agent conversations into automated business outcomes.** These 6 import-ready Copilot Studio workflows bridge the gap between *asking an agent* and *getting things done* — triggers, If/Else logic, AI approvals, human review steps, and M365 connectors, all pre-built and ready to import.

Each workflow ships with: YAML spec, setup guide, test data, and a walkthrough video script (2–3 min for #1–5, 10–15 min for #6) — so you go from download to live in hours, not weeks.

### Why buy vs. build?

| Instead of… | This workflow does it |
|-------------|----------------------|
| Coding a document approval from scratch | AI extracts, validates, routes → human signs off in Teams |
| Triaging IT tickets manually | Agent classifies → escalating with SLA timers |
| Onboarding each new hire line-by-line | Auto-creates accounts, tasks, knowledge handoff |
| Drowning in shared inbox email | AI triages priority, files attachments, digests daily |
| Auditing docs against compliance rules | Validates, flags violations, tracks remediation |
| Guessing at AI token spend | Real-time dashboard + cost tracking + budget alerts |

### Workflow Catalog

| # | Workflow | Pairs With | Complexity |
|---|----------|------------|------------|
| 1 | **Document Approval — AI Pre-check + Human Sign-off** | `legal-compliance-agent.yaml` | Advanced |
| 2 | **IT Ticket Triage & Escalation** | `it-helpdesk-agent.yaml` | Mid |
| 3 | **HR Onboarding Automation** | `onboarding-buddy-agent.yaml` + `hr-policy-agent.yaml` | Advanced |
| 4 | **Email Triage & Daily Digest** | All agents (standalone) | Standard |
| 5 | **Compliance Document Validation** | `legal-compliance-agent.yaml` | Advanced |
| 6 | **AI Spend & Productivity Dashboard** | `agent-cost-intelligence` (nasyhub.com) | Advanced |

See full workflow catalog → [workflows/index.md](workflows/index.md) including bundles, pairing maps, and prerequisites.

## Key Findings from MD Export

- **Model choice:** Claude Opus 5 (via Copilot Studio agent settings)
- **Knowledge source:** SharePoint site (not individual folder — can scope via site)
- **Channels:** Microsoft365Copilot + Teams
- **Memory:** enabled (agent retains conversation context)
- **Web search:** disabled (strict grounding on enterprise data)
- **Authentication:** Integrated (AAD, respects user permissions)
- **Template:** `cliagent-1.0.0` — supports natural-language builder

## Corporate Value Proposition

| Metric | Impact |
|--------|--------|
| Time saved per query | 12-15 min (vs manual searching) |
| Resolution rate | 70-85% from KB (improves with self-learning) |
| Onboarding ramp | 30-50% faster (new hires ask freely) |
| Board-reportable | Every interaction logged → Power BI → FTE-equivalent saved |
| Security-baked | Respects existing M365 permissions |

---

*Created for Nasir Syed portfolio — Enterprise Copilot Agent Templates*