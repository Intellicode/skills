# Early-Stage Valuation

## Table of Contents
- [Overview](#overview)
- [Stage-Based Valuation Ranges](#stage-based-valuation-ranges)
- [Valuation Methods](#valuation-methods)
- [SAFEs and Convertible Notes](#safes-and-convertible-notes)
- [Cap Table Analysis](#cap-table-analysis)
- [Red Flags](#red-flags)

## Overview

Early-stage valuation is more art than science. Unlike public companies with revenue multiples and comparable transactions, early-stage startups are valued based on:

1. **Founder quality and team composition**
2. **Market opportunity size**
3. **Traction and momentum**
4. **Competitive dynamics and deal terms**
5. **Comparable financings in the market**

The right valuation is the one that:
- Gives founders enough runway to hit meaningful milestones
- Provides investors with appropriate return potential (10x+ for early-stage)
- Aligns incentives between founders and investors
- Is defensible relative to comparable deals

## Stage-Based Valuation Ranges

### Pre-Seed ($500K - $2M raise)
| Metric | Typical Range |
|--------|--------------|
| Pre-money valuation | $2M - $6M |
| Instrument | SAFE or Convertible Note |
| Cap | $3M - $8M |
| Key criteria | Team quality, problem authenticity |

### Seed ($1M - $5M raise)
| Metric | Typical Range |
|--------|--------------|
| Pre-money valuation | $5M - $20M |
| Instrument | Priced round or SAFE |
| Key criteria | Team + early traction signals |

### Series A ($5M - $15M raise)
| Metric | Typical Range |
|--------|--------------|
| Pre-money valuation | $15M - $60M |
| Instrument | Priced round (preferred stock) |
| Key criteria | Clear product-market fit evidence, growth metrics |

**Note:** Valuations vary significantly by sector, geography, and market conditions. AI companies in 2024-2025 commanded significant premiums.

## Valuation Methods

### 1. Comparable Transactions Method (Most Common)

Look at recent financings for similar companies at similar stages.

```
Valuation = Comparable deal valuations adjusted for:
  + Team quality premium/discount
  + Market size premium/discount
  + Traction premium/discount
  + Market condition premium/discount
```

**Sources:** PitchBook, Crunchbase, AngelList, Carta, industry reports

### 2. Venture Capital Method

```
Exit valuation = Expected exit value (based on comparables)
Required return multiple = Target fund return (10x+ for early-stage)
Post-money valuation = Exit valuation / Required return multiple
Pre-money valuation = Post-money valuation - Investment amount

Example:
- Expected exit: $500M in 7 years
- Required return: 10x
- Investment: $2M
- Post-money: $500M / 10 = $50M
- Pre-money: $50M - $2M = $48M
```

### 3. Scorecard Method (Pre-Seed / Seed)

Weight and score relative to average deals:

| Factor | Weight |
|--------|--------|
| Team strength | 30% |
| Market size | 25% |
| Product/technology | 15% |
| Competitive environment | 10% |
| Marketing/sales channels | 10% |
| Other (timing, terms) | 10% |

**Score each factor:** 0.5x (terrible) to 2.0x (exceptional)

```
Adjusted valuation = Average valuation × Weighted score

Example:
- Average seed pre-money: $10M
- Team: 1.5x (exceptional founders)
- Market: 1.2x (large, growing)
- Product: 0.8x (early, unproven)
- Competition: 1.0x (average)
- Marketing: 0.9x (untested channels)
- Other: 1.0x
- Weighted score: (1.5×0.30 + 1.2×0.25 + 0.8×0.15 + 1.0×0.10 + 0.9×0.10 + 1.0×0.10)
- = 0.45 + 0.30 + 0.12 + 0.10 + 0.09 + 0.10 = 1.16
- Adjusted pre-money: $10M × 1.16 = $11.6M
```

### 4. Revenue Multiples (Post-Revenue Only)

Only applicable when there is meaningful revenue:

```
Valuation = ARR × Revenue Multiple

SaaS multiples (benchmarks):
- < $1M ARR: 10-30x (based on growth rate)
- $1-5M ARR: 8-20x
- $5-20M ARR: 5-15x

Adjust multiples based on:
  + Growth rate (100%+ growth = premium)
  + Net revenue retention (>120% = premium)
  + Gross margin (>70% for SaaS = premium)
  + Market position and defensibility
```

## SAFEs and Convertible Notes

### SAFE (Simple Agreement for Future Equity)

YC's standard instrument for early-stage investing. Key terms:

**Cap:** Maximum valuation at which the SAFE converts to equity
- Pre-seed caps: $3M - $8M
- Seed caps: $6M - $15M

**Discount:** Percentage discount to next priced round
- Typical: 15-25% (20% is standard)

**Most Favored Nation (MFN):** If the company issues SAFEs with better terms, this SAFE gets those terms too.

**Pro-rata rights:** Right to maintain ownership percentage in future rounds.

### SAFE vs. Convertible Note

| Feature | SAFE | Convertible Note |
|---------|------|------------------|
| Debt instrument | No (equity) | Yes (debt) |
| Interest rate | None | Typical: 5-8% |
| Maturity date | None | Typical: 18-24 months |
| Investor protection | Lower | Higher |
| Founder friendliness | Higher | Lower |

### When SAFEs Are Appropriate
- Pre-seed and seed rounds
- Fast-moving deals where speed matters
- When founders and investors trust each other
- YC company standard practice

### When Priced Rounds Are Appropriate
- Series A and beyond
- When investors need stronger protections
- When significant capital is being invested
- When cap table clarity is important

## Cap Table Analysis

### Key Metrics to Check

| Metric | Good | Warning | Red Flag |
|--------|------|---------|----------|
| Founder ownership (pre-Series A) | > 60% | 40-60% | < 40% |
| Employee option pool | 10-15% | 5-10% or 15-20% | < 5% |
| Investor ownership (pre-Series A) | < 30% | 30-40% | > 40% |
| Dead equity | 0% | < 5% | > 5% |

### Common Cap Table Issues

1. **Dead equity** — Equity held by departed founders, inactive advisors, or early contributors who are no longer contributing. Red flag if >5%.

2. **Misaligned vesting** — Founders should have 4-year vesting with 1-year cliff. No cliff or vesting already earned is concerning.

3. **Over-dilution** — If founders own < 40% pre-Series A, they may lack motivation through the long grind.

4. **Advisory equity** — Advisors should typically get 0.1-0.5%. More than 1% is unusual and concerning.

5. **Unpriced rounds stacking** — Multiple SAFEs without a priced round can create cap table confusion and misaligned incentives.

## Red Flags

- Unreasonable valuation for the stage and traction
- Complex deal structures for early-stage investments
- Reluctance to share cap table
- Large equity positions for non-founders (>5% for any single non-founder)
- No vesting provisions for founders
- Previous down rounds or recapitalization
- Unclear or contested IP ownership
- Significant debt on the balance sheet