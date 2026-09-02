# Document Approval — Expected Extractions & Paths

Use these sample documents to validate the `Extract document fields` prompt node and the policy If/Else branches.

| # | Document | Type | Vendor | Amount | Currency | Confidence | Expected Path | Expected Outcome |
|---|----------|------|--------|--------|----------|------------|---------------|------------------|
| 1 | `sample-invoice.md` | invoice | Acme Office Supplies Pty Ltd | 245.00 | USD | 95 | AI approval | Approved |
| 2 | `sample-expense-report.md` | expense_report | Jane Doe | 6740.50 | USD | 88 | Human review | Pending approver |
| 3 | `sample-contract.md` | contract | Beta Technologies Inc. | 48000.00 | USD | 92 | Human review | Pending approver |

## Validation Steps

1. Import the workflow YAML into Copilot Studio.
2. Configure connection references (SharePoint, Exchange Online, Teams).
3. Set the `docapproval_ThresholdLow` and `docapproval_ThresholdHigh` environment variables.
4. Use **Test this node** on `Extract document fields` for each sample.
5. Verify the extracted JSON matches the Expected Extraction blocks.
6. Trace each result through the `Choose approval path` condition.
7. For the invoice, confirm the `AI approval decision` returns `Approved`.
8. For the expense report and contract, confirm a Teams adaptive card is generated.

## Required Environment Variables

Before running tests, set:

- `docapproval_ThresholdLow`
- `docapproval_ThresholdHigh`
- `docapproval_DefaultCurrency`
- `docapproval_AuditSiteUrl`
- `docapproval_AuditListName`
- `docapproval_ApproverEmail`
- `docapproval_TeamsTeamId`
- `docapproval_TeamsChannelId`
- `docapproval_DocumentLibraryPath`
