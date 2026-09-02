# Compliance Document Validation — Test Data

This folder holds sample inputs and expected outputs for the **Compliance Document Validation** workflow (`#05`).

## Planned test assets

- `sample-acceptable-policy.pdf` — policy document that passes all checks
- `sample-missing-clause.docx` — contract missing a required compliance clause
- `sample-high-risk-vendor.xlsx` — vendor list containing a flagged entity
- `sample-pii-exposure.docx` — document with unredacted PII
- `expected-validation-results.md` — expected AI extraction and risk scores for each sample
- `sample-sharepoint-list.csv` — mock Compliance Validation Log list schema

## Environment

Point the workflow at this folder during local validation:

- `compliance_LibraryUrl` → local SharePoint test site
- Drop sample documents into the test document library
- Run the workflow and compare outputs to `expected-validation-results.md`

> Honey: expand this folder with buyer-facing test data and a short validation checklist.
