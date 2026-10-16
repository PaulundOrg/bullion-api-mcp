---
name: bullion-portfolio-review
description: Review the connected user's Bullion API portfolio using read-only tools, exact decimal values, compatible units and periods, and explicit valuation dates.
---

Use this workflow when the user asks to understand their own Bullion API portfolio. Use only the connected account's API responses and covered read tools; never ask for credentials or copy account data to another service.

1. Start with `get_portfolio`. Use `get_portfolio_lots`, `list_portfolio_transactions`, or `get_portfolio_gains` only when needed to answer the request. Respect each tool's account scope and parameters.
2. Report the response's as-of/valuation date, currency, weight unit, and freshness metadata when supplied. Distinguish transaction dates from valuation dates. If a field or date is missing, mark it unavailable rather than infer it.
3. Preserve API decimal strings for holdings, weights, cost basis, prices, and gains. Quantities and money can use scales 15 and 8; never convert them through JavaScript `Number` or binary floating point. Display prices, costs, P&L, and weights to two decimal places, while retaining source precision for calculations and identifying display rounding.
4. Reconcile or compare values only when currency, weight unit, period, and valuation basis are compatible. Explain any mismatch or limitation; do not infer missing fees, tax treatment, prices, or transactions. Preserve any required public attribution included in a response.
5. Keep the workflow read-only. If asked to create, edit, delete, import, or otherwise change portfolio data, explain that this workflow cannot perform that action. Do not give personalized investment or tax advice.

Summarize holdings and reported costs/gains only to the level supported by the API, with dates and units beside the figures.
