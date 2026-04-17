# Building & Shipping Fast

## Table of Contents
- [YC Building Philosophy](#yc-building-philosophy)
- [Batch Sprint Structure](#batch-sprint-structure)
- [MVP Scoping Framework](#mvp-scoping-framework)
- [Rapid Iteration Playbook](#rapid-iteration-playbook)
- [Product-Market Fit Signals](#product-market-fit-signals)

## YC Building Philosophy

### Core Principles
1. **Ship, then iterate.** Your first version will be wrong. Ship it anyway.
2. **Talk to users.** Not once a month. Every day. Not your mom. Not other founders. Real users with real problems.
3. **Measure.** If you can't measure it, you can't improve it.
4. **Do things that don't scale.** Manual concierge, hand-holding, whatever it takes to learn.
5. **Launch fast.** "Launch" does not mean "public beta with press release." It means put something in front of users.

### The Build-Measure-Learn Cycle
The fastest loop wins. Optimize for cycle time:

```
Build (hours/days) → Measure (hours) → Learn (minutes) → Build again
```

If your loop takes weeks, you're going too slow. Target 24-48 hour cycles during the batch.

### What "Ship" Actually Means
- Users can interact with it (even if it breaks)
- You can measure something (even if the metric is crude)
- You can learn from it (even if the lesson is "this doesn't work")

Perfection is the enemy. A broken thing in users' hands teachest more than a perfect thing in your head.

## Batch Sprint Structure

### Weekly Cadence (Recommended)

**Monday: Plan**
- Review last week's metrics (users, revenue, activation, retention)
- List the 1-2 most important things to ship this week
- Write them down. Share with your group partner.
- Schedule 3-5 user conversations for the week

**Tuesday-Thursday: Build**
- Rapid execution. No meetings except user calls.
- Push code to production at least once per day.
- Ship features in the smallest possible increments.

**Friday: Review & Talk to Users**
- Group office hours (1x per week with YC partner)
- Review what shipped vs. what you planned
- Talk to at least 2-3 users
- Update metrics dashboard

**Saturday: Think**
- Reflect without doing. Are we working on the right thing?
- Read batch-mate updates. Help others; get help.
- Journal what you learned this week.

### 11-Week Batch Timeline

| Week | Focus | Key Activities |
|------|-------|----------------|
| 1-2 | Ship MVP + Talk to Users | Get something live, 10+ user conversations |
| 3-4 | Iterate Based on Feedback | Rapid cycles, fix what breaks, add what users ask for |
| 5-6 | Find Growth Vector | Identify one acquisition channel that works, double down |
| 7-8 | Pressure Test | Is this working? Consider pivot if metrics don't move |
| 9-10 | Polish & Momentum | Lock in your story, prepare Demo Day materials |
| 11 | Alumni Demo Day | Present to YC partners and batch |

## MVP Scoping Framework

### The "Worst Viable Product" Exercise
Instead of asking "what should we build?", ask "what's the worst version of this that still tests our core hypothesis?"

1. **State your hypothesis.** "If we give [specific users] [specific thing], they will [specific action]."
2. **Identify the minimum signal.** What's the simplest thing you could observe that would confirm or deny the hypothesis?
3. **Build only what produces that signal.** Cut everything else.

### Feature Prioritization: The YC Cut
For each proposed feature, ask:

- Does this directly test our core hypothesis? (If no, cut it)
- Can we learn the same thing with less? (If yes, do less)
- Would a user notice if we didn't build this? (If no, cut it)
- Can we do this manually instead? (If yes, do it manually first)

### Scope Reduction Examples
| Instead of | Do this |
|-----------|---------|
| Full auth system | Single password or no auth |
| Payment integration | Manual invoicing (Stripe links) |
| Admin dashboard | Direct database queries |
| Email notifications | Manual emails to first 10 users |
| Search/filter | List everything, users scroll |
| Onboarding flow | Hand-hold first users personally |

## Rapid Iteration Playbook

### The 48-Hour Ship Cycle

**Hour 0-4: Define**
- Pick one thing to learn
- Design the smallest experiment
- Write 1-2 metrics you'll check

**Hour 4-24: Build**
- Write the minimum code
- Deploy immediately when it works at all
- Don't wait for "done"

**Hour 24-36: Observe**
- Watch metrics (even crude ones)
- Talk to 2-3 users who tried it
- Note what surprised you

**Hour 36-48: Decide**
- Double down, iterate, or kill the feature
- If doubling down: what's the next experiment?
- If iterating: what specifically changed?
- If killing: what did you learn? Archive it.

### Common Speed Traps
1. **Over-engineering.** You don't need microservices. You need users.
2. **Design perfectionism.** Your first 100 users don't care about your font choice.
3. **"I'll just add one more thing."** No. Ship what you have.
4. **Analysis paralysis.** Make a decision. If it's wrong, you'll know in 48 hours.
5. **Building for scale you don't have.** If you have 10 users, you have 10 users' problems, not 10M users' problems.

### User Conversation Template
- "Tell me about the last time you [experienced the problem]."
- "What did you do to solve it?"
- "What was frustrating about that?"
- "If you had a magic wand, what would you change?"
- "Would you pay $X for something that solved this?"

**Rules:**
- Listen more than you talk (80/20)
- Never ask "would you use this?" (people lie). Ask "when did you last have this problem?"
- Take notes. Review them weekly.
- Record calls when possible (ask permission).

## Product-Market Fit Signals

### You Don't Have PMF Yet If...
- Users try once and don't come back
- You're pushing, not pulling
- Growth requires continuous marketing spend with no word of mouth
- Retention curves flatten at low levels
- Users say "this is cool" but don't change their behavior

### You Might Have PMF If...
- Users are pulling—asking for features, inviting others, upset if it goes away
- Organic word-of-mouth growth
- Retention curves flatten at high levels (>40% D30 for consumer, >90% M3 for B2B SaaS)
- You can't build fast enough to keep up with demand
- Users find you without you finding them

### The Superhuman PMF Survey
Ask active users: "How disappointed would you be if you could no longer use this product?"
- Very disappointed: 40%+ = strong PMF signal
- Somewhat disappointed
- Not disappointed

If < 40% say "very disappointed," keep iterating.