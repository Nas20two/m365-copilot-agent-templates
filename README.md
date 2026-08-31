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