# Sample Expense Report — Test Document

**Employee:** Jane Doe
**Report date:** 2026-08-20
**Trip:** Client visit to Sydney
**Total amount:** $6,740.50
**Currency:** USD

**Expenses:**
- Flight: $1,200.00
- Hotel (5 nights): $1,850.00
- Meals: $490.50
- Ground transport: $300.00
- Client entertainment: $2,900.00

## Expected Extraction

```json
{
  "docType": "expense_report",
  "vendor": "Jane Doe",
  "amount": 6740.50,
  "currency": "USD",
  "date": "2026-08-20",
  "confidence": 88
}
```

## Expected Approval Path

With default thresholds (Low $500, High $5000):
- Amount $6,740.50 ≥ $5000 → **Human review path**
- Expected action: Teams adaptive card sent to approver
