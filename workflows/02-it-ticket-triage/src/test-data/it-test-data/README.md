# IT Ticket Triage — Test Data

Sample IT helpdesk tickets for validating the workflow's LLM classify and severity branching logic.

---

## Expected Classifications

| # | From | Subject | Category | Severity | Expected Action |
|---|---|---|---|---|---|
| 1 | jane@contoso.com | "Can't log in — password expired" | Password Reset | P3 Medium | Ticket created, 8h SLA |
| 2 | bob@contoso.com | "VPN down — all remote staff affected" | Software | P1 Critical | Teams ping + assignee, ticket, instant SLA |
| 3 | alice@contoso.com | "Need new laptop, old one is failing" | Hardware | P2 High | Ticket created, 4h SLA |
| 4 | sysadmin@contoso.com | "Firewall rule expired, security gap" | Access | P1 Critical | Teams ping + assignee, ticket, instant SLA |
| 5 | hr@contoso.com | "New hire needs Adobe license" | Software | P4 Low | Ticket created, EOD queue |
| 6 | mike@contoso.com | "Cannot access shared drive" | Access | P3 Medium | Ticket created, 8h SLA |
| 7 | sarah@contoso.com | "Keyboard not working on docking station" | Hardware | P4 Low | Ticket created, EOD queue |
| 8 | ceo@contoso.com | "Email not syncing on phone — urgent" | Software | P2 High | Ticket created, 4h SLA |

## Validation Steps

1. Import the workflow YAML into Copilot Studio.
2. Configure connection references (Exchange Online, SharePoint, Teams).
3. Set environment variables to match your test tenant.
4. Use **Test this node** on the `Classify ticket` prompt for each sample.
5. Paste `subject` into the prompt input; verify the category and severity output.
6. Trace each through the `Severity check` condition to confirm the correct action branch.
7. Run an end-to-end test with the P1 Critical sample and confirm a Teams alert fires.

## Required Environment Variables

- `helpdesk_MailboxAddress`
- `helpdesk_TeamsTeamId`
- `helpdesk_TeamsChannelId`
- `helpdesk_TicketsListName`
- `helpdesk_SiteUrl`
