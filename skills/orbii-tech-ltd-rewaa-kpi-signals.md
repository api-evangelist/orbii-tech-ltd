---
name: Retrieve Orbii Rewaa KPI signals
description: Pull the raw KPI signal families (eligibility, revenue, liquidity, stability, seasonal trends) and the active KPI rule thresholds that drive an Orbii Rewaa credit decision.
api: openapi/orbii-tech-ltd-rewaa-openapi.json
operations: [getRewaaBaselineEligibilityRaw, getRewaaRevenueAndSalesPerformanceRaw, getRewaaPaymentProcessingAndLiquidityRaw, getRewaaBusinessStabilityAndRiskRaw, getRewaaIndustryAndSeasonalTrendsRaw, getRewaaKpiRules]
generated: '2026-07-20'
method: generated
source: openapi/orbii-tech-ltd-rewaa-openapi.json
---

# Retrieve Orbii Rewaa KPI signals

Read the underlying credit-KPI signal families Orbii computes for a Rewaa merchant, plus the rule thresholds that map those KPIs to a band. Base `https://api.rewaa.orbii.ai`. All operationIds are verified against `openapi/orbii-tech-ltd-rewaa-openapi.json`.

## Authentication
Pass `user` and `password` as query-string parameters over HTTPS (see `authentication/orbii-tech-ltd-authentication.yml`).

## Steps
1. **Baseline eligibility** — `GET /Rewaa_Baseline_Eligibility_Raw` (`getRewaaBaselineEligibilityRaw`).
2. **Revenue & sales** — `GET /Rewaa_Revenue_And_Sales_Performance_Raw` (`getRewaaRevenueAndSalesPerformanceRaw`).
3. **Payment processing & liquidity** — `GET /Rewaa_Payment_Processing_And_Liquidity_Raw` (`getRewaaPaymentProcessingAndLiquidityRaw`).
4. **Business stability & risk** — `GET /Rewaa_Business_Stability_And_Risk_Raw` (`getRewaaBusinessStabilityAndRiskRaw`).
5. **Industry & seasonal trends** — `GET /Rewaa_Industry_And_Seasonal_Trends_Raw` (`getRewaaIndustryAndSeasonalTrendsRaw`).
6. **Active rule thresholds** — `GET /Rewaa_KPI_Rules` (`getRewaaKpiRules`) to see how the raw KPIs are scored into a band. Adjust with `updateKpiRules` (`POST /UpdateKpiRules`) only when you own the rule configuration.

## Rules
- Errors return a flat `{"error": "..."}` JSON object; see `errors/orbii-tech-ltd-problem-types.yml`.
- These are read (`GET`) signals — safe to fetch repeatedly. Run a fresh assessment (`runAssessment`) first if the underlying data changed.
- See `data-model/orbii-tech-ltd-data-model.yml` for how KPI records relate to a Client/merchant.
