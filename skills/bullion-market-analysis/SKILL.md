---
name: bullion-market-analysis
description: Analyze Bullion API precious-metals observations with read-only tools, exact decimal handling, comparable periods and explicit date and freshness context.
---

Use this workflow for precious-metals price, trend, or market-statistic questions. Use only the connected Bullion API read tools and their returned data.

1. Use `get_metal_price` or `get_metal_price_history` for price observations. For supported gold analysis, use `get_gold_moving_average`, `get_gold_volatility`, `get_gold_drawdown`, or `get_gold_silver_ratio` when relevant. Follow the tool's declared parameters and supported values; ask for missing metal, currency, or period when needed.
2. State each returned value's unit or currency, observation date or covered period, and freshness/cache metadata when provided. Distinguish an observation date from a refresh timestamp. If dates or freshness are absent, say so. Never describe data as real-time or live.
3. Compare series only when their units/currencies, scales, period or frequency, and stated scope/basis/method are compatible. Do not silently convert, annualize, fill missing periods, or infer a cause. Explain when a comparison is not supported.
4. Keep API decimal strings exact for calculations; quantities and money can use scales 15 and 8. Never convert financial values through JavaScript `Number` or binary floating point. Display prices to two decimal places without replacing the source precision; label any rounding.
5. Preserve any public attribution or reuse notice present in the API response, including required notices for public statistics. Do not invent provenance or attribution that the response does not provide.

Give a concise summary, then the evidence and caveats. Treat results as informational, not investment advice or an automated trading signal.
