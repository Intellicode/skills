# Growth & Metrics

## Table of Contents
- [Key Metrics by Stage](#key-metrics-by-stage)
- [Weekly Growth Rate Targets](#weekly-growth-rate-targets)
- [Metric Tracking](#metric-tracking)
- [Growth Experiments Framework](#growth-experiments-framework)
- [User Acquisition Channels](#user-acquisition-channels)
- [Retention Analysis](#retention-analysis)

## Key Metrics by Stage

### Pre-Product-Market Fit (Most of Batch)
Focus on learning metrics, not vanity metrics:

| Metric | What It Tells You | Target |
|--------|-------------------|--------|
| Weekly active users | Are people using it at all? | Growing week over week |
| Activation rate | % of signups who experience value | >25% for B2B, >40% for consumer |
| User conversations/week | Are you talking to users? | 5-10 minimum |
| Ship velocity | How fast are you learning/changing? | Multiple deploys/week |
| Retention (D7/D30) | Does the product stick? | Improving trend |

### Approaching PMF (Weeks 5-8)
Add growth metrics:

| Metric | What It Tells You | Target |
|--------|-------------------|--------|
| Weekly growth rate | Is usage compounding? | 5-7% WoW |
| Net revenue retention | Are customers expanding? | >120% (B2B SaaS) |
| Organic acquisition % | Is word-of-mouth working? | >30% |
| NPS / PMF survey | How much do users care? | >40% "very disappointed" |
| CAC payback | Unit economics signal | <12 months (B2B SaaS) |

### Post-PMF / Scaling
Add efficiency metrics:

| Metric | What It Tells You | Target |
|--------|-------------------|--------|
| LTV:CAC | Unit economics | >3:1 |
| MRR | Revenue momentum | Growing 10%+ MoM |
| Burn rate | Runway | 18+ months runway |
| Net dollar retention | Expansion revenue | >110% |

## Weekly Growth Rate Targets

### YC's Benchmark: 5-7% WoW
- 5% WoW = 2.9x in 3 months
- 7% WoW = 3.6x in 3 months
- 10% WoW = 5.6x in 3 months (exceptional)

### How to Think About Growth Rate
- Percentages matter more when small. Going from 10 to 20 users is 100% growth (but fragile).
- Focus on the trend, not individual weeks.
- Bad weeks happen. Two bad weeks in a row = diagnose the problem.
- Growth rate means different things at different scales: at 100 users, 7% WoW is 7 new users. At 10K, it's 700.

### Growth Rate by Channel
Track growth rate per channel to find what works:

```
Week N Growth Breakdown:
- Organic/search: X new users (Y% WoW growth)
- Referral: X new users (Y% WoW growth)
- Paid: X new users (Y% WoW growth, CAC = $Z)
- Partnerships: X new users (Y% WoW growth)
```

## Metric Tracking

### The Weekly Update (YC Format)
Use the template in [assets/weekly-update-template.md](assets/weekly-update-template.md).

Every week, track and share:
1. **Growth numbers:** Users, revenue, key metric (whichever best reflects your business)
2. **What you shipped:** Features launched this week
3. **What you learned:** From users, data, experiments
4. **Blockers:** What's slowing you down
5. **Next week's focus:** Top 1-2 priorities

### Dashboard Setup
Use PostHog (free for startups), Mixpanel, or a simple spreadsheet:

**Minimum viable dashboard:**
- Total users (cumulative)
- Active users (DAU/WAU/MAU)
- Signups per week
- Activation rate
- Retention cohort chart
- Revenue (if applicable)

**Nice to have:**
- Funnel conversion (signup → activation → retention → revenue)
- Feature usage heatmap
- User segmentation (power vs. casual users)
- Cohort retention table

### Choosing Your North Star Metric
Pick ONE metric that best reflects value delivered to users:

| Business Type | Common North Star |
|--------------|-------------------|
| Marketplace | Transactions completed |
| SaaS | Weekly active users on paid plans |
| Consumer social | DAU or time spent |
| Fintech | Transactions or AUM |
| Developer tools | Daily active developers |
| E-commerce | Monthly active buyers |

## Growth Experiments Framework

### The Experiment Canvas
For each growth experiment, fill out:

```
Hypothesis: If we [action], then [metric] will [change] by [amount].
Experiment: What we'll builtest.
Success metric: How we'll measure if it worked.
Duration: How long we'll run it (1-2 weeks max).
Decision: If it works → [scale it]. If it doesn't → [kill it or iterate].
```

### Experiment Velocity
- Run 1-2 experiments per week during the batch
- Don't run more than 2 at a time (you won't be able to attribute results)
- Each experiment should have a clear pass/fail criterion before you start
- Kill losers fast. Double down on winners.

### Prioritization Quick Framework
Rate each potential experiment:
- **Impact:** If this works, how much does it move the needle? (1-5)
- **Effort:** How long to build and test? (1-5, lower = easier)
- **Learn:** How much will we learn regardless of outcome? (1-5)

Priority = Impact × Learn ÷ Effort. Start with the highest scores.

## User Acquisition Channels

### Channel Selection
Pick ONE primary channel to start. Prove it works before adding others.

**Common channels for YC companies:**

| Channel | Works Best For | Time to Results | Cost |
|---------|----------------|-----------------|------|
| Direct sales / outreach | B2B, high ACV | 1-2 weeks | Low (time) |
| Content / SEO | Developer tools, SaaS | 4-12 weeks | Low (time) |
| Community | Developer tools, consumer social | 4-8 weeks | Low |
| Product Hunt launch | Consumer, developer tools | 1 day | Low |
| Paid (Meta/Google ads) | E-commerce, B2C | 1-2 weeks | High |
| App Store optimization | Mobile consumer | 4-8 weeks | Low |
| Referral program | Consumer, marketplace | 2-4 weeks | Medium |
| Partnerships / integrations | B2B SaaS, developer tools | 4-8 weeks | Low |

### The "Do Things That Don't Scale" Approach
Before optimizing any channel:

1. **Manually recruit users.** Email, call, Slack, in-person. Every early user is hand-recruited.
2. **Delight each user personally.** White-glove onboarding. Fix their problems directly.
3. **Ask for referrals.** "Who else has this problem?"
4. **Build in public.** Tweet, blog, post on HN, Reddit. Share what you're learning.
5. **Go where your users are.** Fish where the fish are. Slack communities, forums, meetups.

Only invest in scalable channels once you've proven demand through unscalable ones.

## Retention Analysis

### Why Retention Matters
- Growth without retention is a leaky bucket
- You can't out-grow bad retention with acquisition
- Retention is the clearest PMF signal

### Reading a Retention Curve
```
Day 0:  100%  ████████████████████████
Day 1:  60%  ██████████████
Day 7:  35%  ████████
Day 14: 28%  ███████
Day 30: 22%  █████
Day 60: 20%  █████   ← This flattening is what matters
Day 90: 19%  █████
```

**Good retention:** Curve flattens above the "alive" line
- B2B SaaS: >90% monthly retention
- Consumer: >25% D30 retention is decent, >40% is strong
- Marketplace: >30% monthly repeat purchase rate

**Bad retention:** Curve keeps declining. Users try, leave, and never come back. This means the product isn't sticky—fix the product before trying to grow.

### Cohort Analysis
Compare retention across cohorts to see if your product is improving:

```
Cohort      D1    D7    D30
January      55%   30%   18%
February     58%   33%   21%  ← improving
March        62%   38%   26%  ← improving more
```

If each cohort retains better than the last, you're building something people want.