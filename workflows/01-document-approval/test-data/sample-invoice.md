# Sample Invoice — Test Document

**Document type:** invoice
**Vendor:** Acme Office Supplies Pty Ltd
**Invoice number:** INV-2026-0442
**Invoice date:** 2026-08-15
**Due date:** 2026-09-15
**Amount:** $245.00
**Currency:** USD
**Line items:**
- 5x Ergonomic chairs @ $49.00 each

## Expected Extraction

```json
{
  "docType": "invoice",
  "vendor": "Acme Office Supplies Pty Ltd",
  "amount": 245.00,
  "currency": "USD",
  "date": "2026-08-15",
  "confidence": 95
}
```

## Expected Approval Path

With default thresholds (Low $500, High $5000):
- Amount $245.00 ≤ $500 → **AI auto-approval path**
- Expected outcome: **Approved**
