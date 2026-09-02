# Email Triage — Expected Classifications

Use these rows to validate the AI classify node after import.

| # | From | Subject | Expected Priority | Expected Action |
|---|------|---------|-------------------|-----------------|
| 1 | legal@contoso.com | URGENT: Service outage affecting payroll | Critical | Teams alert + Outlook assignee notification |
| 2 | support@acme-corp.com | Invoice #4482 overdue — vendor threatening hold | High | Teams alert + Outlook assignee notification |
| 3 | hr@company.com | Updated remote-work policy attached | Medium | Add to daily digest only |
| 4 | noreply@newsletter.com | Weekly industry roundup | Low | File attachment (if any) + archive |
| 5 | ceo@company.com | Board meeting materials — need review today | Critical | Teams alert + Outlook assignee notification |

## Validation Steps

1. Import the workflow YAML into Copilot Studio.
2. Configure connection references (Exchange Online, Teams, SharePoint).
3. Set environment variables to match your test tenant.
4. Use **Test this node** on the `Classify email priority` step.
5. Paste each `body_preview` and `subject` into the test inputs.
6. Assert the output matches the expected priority.
7. Run an end-to-end test with one Critical and one Low email.
