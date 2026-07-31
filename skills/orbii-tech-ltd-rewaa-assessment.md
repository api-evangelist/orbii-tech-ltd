---
name: Run an Orbii Rewaa credit assessment
description: Trigger the Orbii assessment pipeline for a Rewaa merchant, then read risk assessment, final band classification, and suggested loan amounts.
api: openapi/orbii-tech-ltd-rewaa-openapi.json
operations: [runAssessment, getRewaaRiskAssessment, getRewaaFinalBandClassification, getRewaaLoanAmounts]
generated: '2026-07-20'
method: generated
source: openapi/orbii-tech-ltd-rewaa-openapi.json
---

# Run an Orbii Rewaa credit assessment

Use the Orbii Rewaa deployment (base `https://api.rewaa.orbii.ai`) to score a merchant and read the resulting lending decision. All operationIds below are verified against `openapi/orbii-tech-ltd-rewaa-openapi.json`.

## Authentication
Orbii declares no OAuth/securityScheme. Requests authenticate by passing `user` and `password` as query-string parameters (see `authentication/orbii-tech-ltd-authentication.yml`). Send them over HTTPS only; never log the query string.

## Steps
1. **Trigger the pipeline** — `POST /Run_Assessment` (`runAssessment`). This runs data ingestion, KPI computation, risk scoring, and band classification. Wait for completion before reading downstream results.
2. **Read risk assessment** — `GET /Rewaa_Risk_Assessment` (`getRewaaRiskAssessment`) to retrieve the computed risk signals.
3. **Read the band** — `GET /Rewaa_Final_Band_Classification` (`getRewaaFinalBandClassification`) for the final credit band.
4. **Read suggested loan** — `GET /Rewaa_Loan_Amounts` (`getRewaaLoanAmounts`) for the recommended loan amount tied to the band. Use `POST /Rewaa_Loan_Amounts` (`rebuildRewaaLoanAmounts`) only if you need to force a recompute.

## Rules
- Errors return a flat `{"error": "..."}` JSON object (not RFC 9457). Treat any 4xx/5xx as terminal; see `errors/orbii-tech-ltd-problem-types.yml`.
- No idempotency key is supported — do not blindly retry `runAssessment`; poll the read endpoints instead.
- Paginated endpoints use `page` / `page_size` (see `conventions/orbii-tech-ltd-conventions.yml`).
