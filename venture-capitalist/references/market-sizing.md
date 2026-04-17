# Market Sizing Framework

## Table of Contents
- [Overview](#overview)
- [Bottom-Up Sizing (Preferred)](#bottom-up-sizing-preferred)
- [Top-Down Sizing (Supporting)](#top-down-sizing-supporting)
- [TAM / SAM / SOM Framework](#tam--sam--som-framework)
- [Market Dynamics](#market-dynamics)
- [Common Mistakes](#common-mistakes)

## Overview

Market sizing answers one question: **"Is this opportunity big enough to matter?"**

For early-stage investing, bottom-up sizing is strongly preferred over top-down. YC's philosophy: if you can count your customers, count them. If you can't, estimate conservatively.

## Bottom-Up Sizing (Preferred)

### Formula

```
Market = (# of target customers) × (average revenue per customer)
```

### Step-by-Step

1. **Define the target customer precisely**
   - Who specifically has this problem?
   - What criteria make someone a target customer?
   - How many of these customers exist?

2. **Estimate realistic penetration**
   - How many customers can you reach in year 1? Year 3? Year 5?
   - What adoption barriers exist?

3. **Determine pricing**
   - What do customers currently pay to solve this problem?
   - What willingness-to-pay evidence exists?
   - What's the natural price point?

4. **Calculate**

```
Example: B2B SaaS for dental practices
- Target customers: 200,000 dental practices in the US
- Realistic penetration in year 5: 5% = 10,000 practices
- Average revenue per practice: $500/month = $6,000/year
- Year 5 revenue: 10,000 × $6,000 = $60M ARR
```

### When Bottom-Up Works Best
- B2B businesses with identifiable customers
- Markets with clear pricing benchmarks
- Products replacing existing spending

## Top-Down Sizing (Supporting)

### Formula

```
Market = Total market size × Market share percentage
```

### Use As Validation, Not Primary Method

Top-down sizing is useful for sanity-checking bottom-up numbers:

```
Example validation:
- Bottom-up: $60M ARR in year 5
- US dental software market: $2.4B (reported by Gartner)
- $60M would be 2.5% market share → plausible
```

### Dangers of Top-Down

"We just need 1% of this $50B market" is not a thesis. It's a red flag.

Problems:
- Total market includes segments you can't reach
- 1% is harder than it sounds
- Ignores what customers actually pay
- Does not account for competition, distribution, or timing

## TAM / SAM / SOM Framework

### TAM (Total Addressable Market)
The total revenue opportunity if you captured 100% of your target market.

**Calculate:** Total number of target customers × average annual revenue per customer

```
Example: Task management for remote teams
- 300M knowledge workers globally
- × $120/year average SaaS spend per worker on productivity tools
- = $36B TAM
```

### SAM (Serviceable Addressable Market)
The portion of TAM you can realistically reach with your business model and distribution.

**Calculate:** Subset of TAM based on geography, pricing tier, channel, and product fit

```
Example: By geography and channel
- 50M remote knowledge workers in English-speaking markets
- × $120/year
- = $6B SAM
```

### SOM (Serviceable Obtainable Market)
The portion of SAM you can realistically capture in the next 3-5 years.

**Calculate:** SAM × realistic market share percentage based on competitive dynamics, resources, and timing

```
Example:
- Assume 2-5% capture of SAM in 5 years
- $6B × 3% = $180M in revenue
- This suggests a potential $1B+ outcome at 5x revenue multiple
```

### Validation Check

Ask these questions:
1. Does SOM support the return multiple needed for the fund? (Minimum 10x for early-stage)
2. Is SOM consistent with the company's growth trajectory?
3. Is penetration rate realistic vs. comparable companies?
4. Does the pricing assumption align with customer willingness to pay?

## Market Dynamics

### Market Timing ("Why Now?")

Evaluate timing factors:

| Factor | Examples |
|--------|----------|
| Technology shift | Mobile, AI, cloud adoption |
| Regulatory change | New compliance requirements, deregulation |
| Behavioral shift | Remote work, digital-first consumers |
| Infrastructure availability | APIs, SDKs, platforms that enable new products |
| Demographic change | Gen Z entering workforce, aging population |

### Market Growth Rate

- **Hypergrowth (>50% YoY):** Can create outsized outcomes even with small initial market
- **Growing (10-50% YoY):** Healthy, but need strong competitive position
- **Stable (0-10% YoY):** Only invest if taking significant share from incumbents
- **Declining (<0% YoY):** Generally avoid unless major disruption thesis

### Market Structure

- **Fragmented markets** (many small players): Good for disruption, consolidation plays
- **Concentrated markets** (few dominant players): Harder but can work with a wedge
- **Winner-take-all markets**: High risk, high reward. Network effects critical.
- **Winner-take-most markets**: More common. Multiple players can succeed.

## Common Mistakes

1. **Confusing TAM with opportunity** — A $50B market doesn't mean $50B in opportunity for this startup
2. **Using top-down as primary method** — "1% of $50B" is not a thesis
3. **Ignoring competition for the same customers** — You're not the only one targeting them
4. **Assuming market share without distribution plan** — How will customers find you?
5. **Overlooking market expansion** — Great companies expand their market (Amazon started with books)
6. **Ignoring customer willingness to pay** — The problem exists, but will they pay to solve it?
7. **Counting unwilling customers** — Not everyone with the problem will buy; filter aggressively
8. **Seasonal or cyclical markets** — Annualize carefully, account for cycles