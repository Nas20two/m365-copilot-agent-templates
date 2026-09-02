# Compliance Document Validation — Test Data

Sample documents and expected validation results for the **Compliance Document Validation** workflow (#05).

---

## Sample Documents & Expected Results

| # | Document | Risk Score | Violation Type | Expected Path | Expected Outcome |
|---|---|---|---|---|---|
| 1 | `sample-acceptable-policy.md` | 5 / 100 | None | Auto-approve | Approved |
| 2 | `sample-missing-clause.md` | 42 / 100 | Missing Data Retention Clause | Human review (standard) | Pending legal review |
| 3 | `sample-high-risk-vendor.md` | 78 / 100 | Flagged Vendor Entity | Human review (urgent) | Pending legal review |
| 4 | `sample-pii-exposure.md` | 91 / 100 | Unredacted PII — GDPR Article 33 | Human review (urgent) | Pending legal review |
| 5 | `sample-expired-certification.md` | 65 / 100 | Expired Compliance Certification | Human review (standard) | Pending legal review |

---

## Sample 1: Acceptable Policy Document

`sample-acceptable-policy.md`

```
# Data Handling Policy — ACME Corp, 2026

Effective: 2026-01-15

## 1. Data Classification
All company data is classified as Internal, Confidential, or Restricted.
Each classification has defined handling, storage, and retention requirements.

## 2. Retention Schedule
- Internal data: 3 years
- Confidential data: 7 years
- Restricted data: 10 years

## 3. Access Control
Access is granted on a need-to-know basis and reviewed quarterly.

## 4. Breach Notification
Security incidents involving personal data are reported to the DPO within 24 hours.

---
Reviewed by: Legal Department
Last audit: 2026-06-01
Certifications: SOC 2 Type II, ISO 27001:2022
```

**Expected validation:**
- **Risk score:** 5 (all policy requirements met)
- **Violations:** None
- **Path:** Auto-approve
- **Audit log:** Approved — no remediation needed

---

## Sample 2: Missing Data Retention Clause

`sample-missing-clause.md`

```
# Vendor Data Processing Agreement — DataStream Inc.

Effective: 2026-03-01

## 1. Scope
DataStream Inc. will process customer data for analytics services.

## 2. Data Categories
Processed data includes: customer name, email, usage metrics, and billing history.

## 3. Security Measures
- Encryption at rest (AES-256)
- Encryption in transit (TLS 1.3)
- Quarterly penetration testing

## 4. Sub-processing
DataStream may engage sub-processors with 30-day written notice.

---
No data retention or deletion schedule defined.
No breach notification clause.
```

**Expected validation:**
- **Risk score:** 42
- **Violations:** Missing Data Retention Clause, Missing Breach Notification Clause
- **Path:** Human review (standard)
- **Audit log:** Flagged — pending legal review

---

## Sample 3: High-Risk Vendor

`sample-high-risk-vendor.md`

```
# Master Services Agreement — NovaTech Global

Effective: 2026-07-01

## Services
NovaTech will provide cloud infrastructure and managed Kubernetes operations.

## Data Processing
NovaTech will have access to production databases containing PII.

## Security
- SOC 2 report provided (dated 2025-03 — expired)
- No ISO 27001 certification
- Two data breaches reported in 2025

---
Registered in: Cayman Islands
Entity type: Private Limited
```

**Expected validation:**
- **Risk score:** 78
- **Violations:** Flagged Vendor Entity (high-risk jurisdiction, expired certifications, breach history)
- **Path:** Human review (urgent)
- **Audit log:** Flagged — urgent legal review

---

## Sample 4: PII Exposure

`sample-pii-exposure.md`

```
# Employee Wellness Program — 2026 Q3 Report

Prepared by: HR Department

## Participant Summary
Total participants: 1,247

## Detailed Data (per participant)
- Name: John Smith
- SSN: 123-45-6789
- DOB: 1985-03-14
- Medical condition: Hypertension
- Prescription: Metformin 500mg
- Emergency contact: Jane Smith, +1 (555) 987-6543

[Additional 1,246 records follow the same format — names, SSNs, DOBs, medical conditions, prescriptions, emergency contacts]
```

**Expected validation:**
- **Risk score:** 91
- **Violations:** Unredacted PII — SSN, Medical Data — GDPR Article 33 / HIPAA
- **Path:** Human review (urgent)
- **Audit log:** Flagged — urgent legal review, remediation required

---

## Sample 5: Expired Certification

`sample-expired-certification.md`

```
# Security Posture Report — FinServe Solutions

Effective: 2025-11-01 (expired)

## Certifications Listed
- SOC 2 Type II: Issued 2024-03, Expires 2025-03 (EXPIRED)
- ISO 27001: Issued 2023-06, Expires 2025-06 (EXPIRED)
- PCI DSS: Not applicable

## Current Security Controls
- Encryption: AES-256
- Access control: RBAC
- Audit logging: Enabled
- Incident response: Plan exists, last tested 2024-08

Security controls are current, but certifications have expired.
```

**Expected validation:**
- **Risk score:** 65
- **Violations:** Expired Compliance Certification (SOC 2, ISO 27001)
- **Path:** Human review (standard)
- **Audit log:** Flagged — pending legal review

---

## Validation Steps

1. Import the workflow YAML into Copilot Studio.
2. Configure connection references (SharePoint, Exchange Online, Teams).
3. Set environment variables to match your test tenant.
4. Use **Test this node** on the `Validate document` prompt for each sample.
5. Compare the returned risk score and violation type against the expected values above.
6. Trace each sample through the `Risk branching` condition — verify correct path (auto-approve vs human review).
7. Run an end-to-end test with `sample-pii-exposure.md` and confirm:
   - Risk score ≥ 75
   - Teams alert sent to legal review channel
   - Email notification sent to legal reviewer
   - Remediation task created in SharePoint
   - Audit log entry created with full chain

## Required Environment Variables

- `compliance_LibraryUrl`
- `compliance_AuditListName`
- `compliance_LegalReviewerEmail`
- `compliance_RiskThreshold` (recommended: 30 for testing — lower than default 50 to catch medium risks)
