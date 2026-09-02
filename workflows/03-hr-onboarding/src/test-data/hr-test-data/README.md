# HR Onboarding — Test Data

Sample new hire records for validating the workflow's trigger, welcome email, Planner task creation, and 30/60/90-day check-in automation.

---

## Sample New Hire Profiles

### Profile 1: Standard Corporate Hire

| Field | Value |
|---|---|
| Name | Sarah Chen |
| Email | sarah.chen@contoso.com |
| Department | Engineering |
| Role | Senior Software Engineer |
| Start Date | 2026-10-01 |
| Manager | Ravi Patel |
| Buddy Assigned | TBD |
| Location | HQ — Building A, Floor 4 |

**Expected Automation:**
- ✅ Welcome email sent with onboarding kit link, IT equipment instructions, and manager introduction
- ✅ Planner tasks created:
  - IT Provisioning: Laptop (MacBook Pro), monitors (2x), peripherals, dev environment access
  - Facilities: Badge, desk assignment (A4-312), parking pass
  - Buddy: Welcome plan, first-week check-in schedule
- ✅ Onboarding Buddy Agent handoff triggered (Day 1)
- ✅ 30-day check-in: verify Sarah's team integration and tool access
- ✅ 60-day check-in: mid-point review of ramp-up goals
- ✅ 90-day check-in: performance review scheduling

---

### Profile 2: Remote Contractor

| Field | Value |
|---|---|
| Name | Marcus Johnson |
| Email | marcus.j@external-contoso.com |
| Department | Professional Services |
| Role | Implementation Consultant |
| Start Date | 2026-09-15 |
| Manager | Elena Torres |
| Buddy Assigned | David Kim |
| Location | Remote — Austin, TX |

**Expected Automation:**
- ✅ Welcome email sent with remote onboarding kit (VPN, collaboration tools, time tracking)
- ✅ Planner tasks created:
  - IT Provisioning: Security-tuned laptop, VPN certificate, client-facing tool access
  - Facilities: Remote desk policy acknowledgment (no badge/desk needed)
  - Buddy: Virtual welcome plan, daily 15-min syncs for first week
- ✅ 30-day check-in: remote productivity assessment
- ✅ 60-day check-in: client engagement feedback
- ✅ 90-day check-in: contract extension review

---

### Profile 3: Executive Hire

| Field | Value |
|---|---|
| Name | Dr. Amara Okafor |
| Email | amara.okafor@contoso.com |
| Department | Executive |
| Role | VP of Data Science |
| Start Date | 2026-11-01 |
| Manager | CEO |
| Buddy Assigned | Board liaison |
| Location | HQ — Executive Suite |

**Expected Automation:**
- ✅ Welcome email with executive onboarding briefing, board materials, direct reports calendar
- ✅ Planner tasks created:
  - IT Provisioning: High-end workstation, secure comms, data lake access
  - Facilities: Executive office, parking reserved, building access (all floors)
  - Buddy: Board liaison introduction, org structure walk-through
- ✅ Benefits Q&A via HR Policy Agent (equity, deferred comp, exec benefits)
- ✅ 30-day check-in: strategic initiative review
- ✅ 60-day check-in: team structure assessment
- ✅ 90-day check-in: board presentation prep

---

## Validation Steps

1. Add each profile as a row in the New Hires SharePoint list.
2. Confirm the workflow triggers on list item creation.
3. Verify the welcome email is sent with the correct name and start date.
4. Check Planner plan for created tasks — verify bucket assignment and due dates.
5. Simulate Day 1 and confirm agent handoff fires.
6. Back-date StartDate to test 30/60/90-day check-in recurrence.

## Required Environment Variables

- `hr_NewHiresListName`
- `hr_SiteUrl`
- `hr_WelcomeSenderEmail`
- `hr_ITContactEmail`
- `hr_PlannerPlanId`
- `hr_BuddyListName`
