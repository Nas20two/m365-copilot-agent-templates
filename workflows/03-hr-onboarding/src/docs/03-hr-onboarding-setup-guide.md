# HR Onboarding Automation — Setup Guide


End-to-end new hire onboarding. Fires welcome emails, assigns Planner tasks, hands off to onboarding + HR policy agents, automates 30/60/90-day check-ins.

---

## What's Included

| Deliverable | File | Status |
|---|---|---|
| YAML spec | `src/workflow/03-hr-onboarding-workflow.yaml` | 📝 Atom building |
| Setup guide | This file | ✅ Complete |
| Test data | `src/test-data/hr-test-data/` — sample new hire records & expected task outputs | ✅ Complete |
| Setup video script | `src/video/script.md` | 📝 Coming soon |

---

## Requirements

| Item | Detail |
|---|---|
| License | Copilot Studio + M365 Copilot (for agent handoff triggers) |
| Connectors | SharePoint, Exchange Online, Microsoft Planner, Teams — all **standard** |
| SharePoint | New Hires list + onboarding dashboard lists |
| Planner | Plan + buckets for onboarding tasks (IT, Facilities, Buddy) |
| Teams | HR channel for notifications |
| Agents | `onboarding-buddy-agent.yaml` + `hr-policy-agent.yaml` for conversational handoff |

---

## Environment Variables

Set these in Copilot Studio after import:

| Variable | Example | Purpose |
|---|---|---|
| `hr_NewHiresListName` | `New Hires` | SharePoint list or Forms response source for new hire records |
| `hr_SiteUrl` | `https://contoso.sharepoint.com/sites/HR` | SharePoint site containing the new-hires list |
| `hr_WelcomeSenderEmail` | `hr@contoso.com` | Email address sending automated welcome messages |
| `hr_ITContactEmail` | `it-provisioning@contoso.com` | IT contact for equipment-provisioning tasks |
| `hr_PlannerPlanId` | `<PLANNER_PLAN_ID>` | Planner plan containing onboarding task buckets |
| `hr_BuddyListName` | `Buddy Assignments` | SharePoint list tracking buddy/mentor assignments |

---

## Connection References

| Connection | Connector | Purpose |
|---|---|---|
| `hr_ExchangeOnlineConnection` | `shared_office365` | Send welcome emails + 30/60/90-day check-in messages |
| `hr_SharePointConnection` | `shared_sharepointonline` | Read new hire list, write to dashboard + buddy list |
| `hr_PlannerConnection` | `shared_planner` | Create and assign onboarding tasks per role |
| `hr_TeamsConnection` | `shared_teams` | Post new-hire notification to HR channel |

---

## Setup (at a glance)

1. **Import YAML** into Copilot Studio
2. **Configure connection references** — Exchange Online, SharePoint, Planner, Teams
3. **Set environment variables** — site URL, list names, welcome sender, IT contact
4. **Create SharePoint lists:**
   - `New Hires` — trigger list with columns: Name, Email, StartDate, Department, Role, Buddy
   - `Buddy Assignments` — mapping: NewHireName, BuddyName, StartDate, Status
   - `Onboarding Dashboard` — aggregate status: Phase (Welcome / IT / Facilities / Check-in), Status, DueDate
5. **Create Planner plan** with buckets: IT Provisioning, Facilities Setup, Buddy Plan, HR Check-in
6. **Deploy paired agents** — `onboarding-buddy-agent.yaml` and `hr-policy-agent.yaml`
7. **Load test data** from `src/test-data/hr-test-data/` and run validation
8. **Activate** the workflow (scheduled or event-driven)

---

## Logic Flow

```
New hire record created → Welcome email (Outlook)
                      ↓
           Planner tasks created:
           - IT: equipment provisioning
           - Facilities: badge + desk
           - Buddy: welcome plan
                      ↓
           Onboarding Buddy Agent handoff
           (conversational welcome + FAQ)
                      ↓
           Benefits Q&A via HR Policy Agent
                      ↓
           30/60/90-day scheduled check-ins
                      ↓
           Completion dashboard → HR SharePoint
```

---

## Test Plan

1. **Unit: New hire trigger** — Add a row to the New Hires list. Verify workflow starts.
2. **Unit: Welcome email** — Confirm email is sent with correct name, start date, and department.
3. **Unit: Planner tasks** — Verify IT, Facilities, Buddy tasks created with correct assignees and due dates.
4. **Integration: End-to-end** — Add a full new hire profile. Trace through welcome → tasks → agent handoff → dashboard update.
5. **Regression: 30-day check-in** — Back-date a start date and confirm the scheduled check-in fires.

---

## Troubleshooting

| Symptom | Likely Cause | Fix |
|---|---|---|
| Workflow not firing on new hire | SharePoint trigger not configured for list | Verify `hr_NewHiresListName` matches the actual list name |
| Planner tasks not created | Planner connection not authorized or plan ID mismatch | Re-authenticate `hr_PlannerConnection`; confirm `hr_PlannerPlanId` |
| Welcome email not sending | Sender mailbox not configured | Verify `hr_WelcomeSenderEmail` is a valid licensed mailbox |
| Agent handoff fails | Agent YAML not deployed or mismatched trigger topic | Deploy the paired agents; verify agent trigger topic matches workflow event |
| Dashboard not updating | SharePoint list column names mismatch | Ensure dashboard list columns match workflow expectations |

---

## Pricing Rationale

$79 matches Document Approval as the co-anchor — justified by four-connector orchestration (Exchange, SharePoint, Planner, Teams), dual agent handoff, and 30/60/90-day scheduled check-ins that require a more complex recurrence model.

*Pairs with: `onboarding-buddy-agent.yaml` + `hr-policy-agent.yaml`*
