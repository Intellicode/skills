# Ideation

## Table of Contents

- [Principles](#principles)
- [Techniques](#techniques)
- [Concept Evaluation](#concept-evaluation)
- [Prioritization Frameworks](#prioritization-frameworks)
- [Facilitation Guide](#facilitation-guide)

## Principles

1. **Separate divergence from convergence.** Never evaluate during ideation. Generate first, judge later.
2. **Build on ideas.** "Yes, and..." not "No, but..."
3. **Quantity breeds quality.** The first 10 ideas are obvious. Ideas 30-50 are where novelty lives.
4. **Constraints fuel creativity.** "Design for a billion users" is paralyzing. "Design for one specific person" is liberating.
5. **Timebox everything.** No open-ended brainstorming. Set a clock.

## Techniques

### Crazy 8s

Rapid sketching to generate many ideas quickly. Best for UI/layout exploration.

1. Fold a sheet of paper into 8 sections
2. Set a timer for 8 minutes
3. Sketch one distinct idea per section (1 minute each)
4. No polish — rough sketches only
5. After 8 minutes, review and star the 2-3 strongest ideas

### How Might We (HMW)

Reframe problems into opportunity statements. Best for bridging Define → Ideate.

**Pattern:** `HMW [action verb] [user] to [outcome] despite [constraint]?`

Example: "Users lose interest during onboarding" → HMW make the first 60 seconds so compelling that users forget they're signing up?

Rules:
- Start with HMW (not "Can we..." which implies yes/no)
- Be broad enough for multiple solutions, narrow enough to be actionable
- Neither too generic ("HMW improve the experience?") nor too solution-specific ("HMW add a skip button?")

### SCAMPER

Systematically transform an existing concept. Best when you have a starting idea and need variations.

| Letter | Technique | Prompt |
|--------|-----------|--------|
| S | Substitute | What if we swapped [component] with [alternative]? |
| C | Combine | What if we merged [feature A] with [feature B]? |
| A | Adapt | What if we borrowed [pattern] from [other domain]? |
| M | Modify | What if we made [aspect] bigger/smaller/faster/slower? |
| P | Put to other use | What if this solved [different problem]? |
| E | Eliminate | What if we removed [feature] entirely? |
| R | Reverse | What if the user did this in the opposite order? |

### Worst Idea

Generate deliberately terrible ideas, then invert them. Best for breaking creative blocks.

1. Frame the challenge: "Design the worst possible [experience]"
2. Generate 10 terrible ideas (5 minutes)
3. For each bad idea, ask: "What makes this terrible?"
4. Invert: "How might we achieve the opposite?"

### Dot Voting

Quick group prioritization after ideation. Best for narrowing a large set of ideas.

1. Give each participant 3-5 dot stickers
2. Participants place dots on their preferred ideas (can put multiple on one)
3. Ideas with the most dots advance to evaluation
4. Optional: Use different colored dots for different criteria (impact, feasibility, delight)

###Storyboarding

Map a user's experience across time to find design opportunities. Best for identifying touchpoints and gaps.

1. Define the scenario (who, what, why)
2. Sketch 6-8 frames showing the key moments
3. Include emotional arc (frustration → resolution → satisfaction)
4. Identify where the product enters and exits the story
5. Note moments of friction or delight

## Concept Evaluation

After generating ideas, evaluate systematically:

### Impact vs. Effort Matrix

Plot each concept on a 2x2 grid:

| | Low Effort | High Effort |
|---|---|---|
| **High Impact** | Quick wins | Major projects |
| **Low Impact** | Fill-ins | Avoid |

Prioritize: Quick wins → Major projects → Fill-ins → Avoid

### Six Thinking Hats

Evaluate a concept from multiple perspectives:

| Hat | Focus | Key Questions |
|-----|-------|---------------|
| White | Facts | What data supports this? What do we know? |
| Red | Feelings | How do users feel about this? Gut reaction? |
| Black | Risks | What could go wrong? Why might this fail? |
| Yellow | Benefits | What's the best case? Why will this work? |
| Green | Creativity | What variations could improve this? |
| Blue | Process | What's the next step? Are we missing anything? |

### Design Critique Checklist

- Does it solve the stated problem?
- Does it align with user research insights?
- Is it consistent with existing patterns (or deliberately breaking them)?
- Can a first-time user figure it out without explanation?
- Does it handle edge cases and error states?
- Is it accessible?

## Prioritization Frameworks

### RICE

| Factor | Description |
|--------|-------------|
| **Reach** | How many users will this impact? (per time period) |
| **Impact** | How much does it affect each user? (0.25=minimal, 0.5=low, 1=medium, 2=high, 3=massive) |
| **Confidence** | How certain are we? (100%=high confidence, 80%=medium, 50%=low) |
| **Effort** | How many person-months? (lower = better) |

**Score:** `(Reach × Impact × Confidence) / Effort`

### Kano Model

Categorize features by how they affect satisfaction:

| Type | Definition | Strategy |
|------|------------|----------|
| **Must-have** | Expected baseline. Absence causes dissatisfaction. | Build first. No negotiation. |
| **Performance** | More = better. Satisfaction scales with quality. | Invest proportionally to impact. |
| **Delight**** | Unexpected value. Presence delights, absence doesn't hurt. | Sprinkle in, don't over-invest. |

How to classify: Ask users two questions — "How would you feel if this feature existed?" and "How would you feel if it didn't?" — then map on the 2D grid.

### MoSCoW

Simple, fast prioritization for teams:

| Category | Meaning | Allocation |
|----------|---------|------------|
| **Must** | Non-negotiable for launch | ~60% of effort |
| **Should** | Important but workable without | ~20% |
| **Could** | Nice to have if time allows | ~15% |
| **Won't** | Explicitly excluded this cycle | ~5% |

## Facilitation Guide

### Running an Ideation Session

**Before (5 min):**
1. State the problem clearly (read the HMW statement)
2. Share relevant research insights (2-3 key findings)
3. Set rules: quantity over quality, build on ideas, no evaluation yet

**During (20-30 min):**
1. Start with individual ideation (5 min silent)
2. Share and build on each other's ideas (10 min)
3. Do a second round, pushing for more radical ideas (10 min)
4. If energy drops, inject a technique (Crazy 8s, Worst Idea, SCAMPER)

**After (15 min):**
1. Cluster similar ideas
2. Dot vote to narrow
3. Evaluate top concepts using one framework
4. Assign next steps: who prototypes what, by when

### Remote Adaptation

- Use a digital whiteboard (Miro, FigJam, Mural)
- Run Crazy 8s on individual slides, then gallery walk
- Use emoji reactions instead of dot stickers
- Break into smaller groups (3-4) in breakout rooms, then reconvene