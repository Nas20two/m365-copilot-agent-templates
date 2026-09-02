# Sample Contract — Test Document

**Document type:** contract
**Counterparty:** Beta Technologies Inc.
**Contract number:** CTR-2026-0091
**Effective date:** 2026-09-01
**Term:** 12 months
**Value:** $48,000.00
**Currency:** USD

## Expected Extraction

```json
{
  "docType": "contract",
  "vendor": "Beta Technologies Inc.",
  "amount": 48000.00,
  "currency": "USD",
  "date": "2026-09-01",
  "confidence": 92
}
```

## Expected Approval Path

- Document type is `contract` → **Human review path (no AI approval)**
- Expected action: Teams adaptive card sent to legal/compliance approver
