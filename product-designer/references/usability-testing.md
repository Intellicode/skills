# Usability Testing

## Table of Contents

- [Planning a Test](#planning-a-test)
- [Test Script Template](#test-script-template)
- [Moderation Techniques](#moderation-techniques)
- [Remote Testing](#remote-testing)
- [Analysis and Reporting](#analysis-and-reporting)

## Planning a Test

### What to Test

Define 1-3 specific research questions. Don't test everything at once.

| Test Type | Questions It Answers | Fidelity Needed |
|-----------|---------------------|-----------------|
| **Comprehension** | Do users understand what this is and what they can do? | Low to mid |
| **Task completion** | Can users accomplish specific goals? | Mid to high |
| **Efficiency** | How fast/click-efficient is the design? | High |
| **Satisfaction** | How does the experience feel? | High |
| **Comparison** | Which version performs better? | Matched fidelity |

### Sample Size

- **Qualitative (find issues):** 5 users find 85% of usability problems. This is usually sufficient.
- **Quantitative (measure performance):** 20+ users for statistical significance on completion rates, time-on-task.
- **Comparative (A/B test):** 40+ users per variant for meaningful comparison.

### Recruiting Participants

1. **Define screener criteria** based on your target user:
   - Must-have characteristics (e.g., "manages a team of 5+")
   - Must-not-have characteristics (e.g., "works in UX")
   - Experience level (novice, intermediate, expert)

2. **Recruit from your users** when possible. For early/unlaunched products, recruit from the target demographic.

3. **Compensate fairly:** $50-75 for 30 min, $100-150 for 60 min (US rates; adjust for local market).

4. **Over-recruit by 20%.** No-shows happen. Schedule backups.

5. **Screen out UX professionals, competitive researchers, and people who've done usability tests recently** (within 6 months).

## Test Script Template

```
# Usability Test: [Feature/Product Name]

## Test Objectives
[2-3 specific questions this test will answer]

## Participant profile
- Who: [Target user description]
- How many: [N]

## Introduction (2 min)
"Thank you for participating. I'm [name], and we're testing [product/feature], not you. There are no wrong answers. Your honest feedback helps us improve. This session will take about [duration] minutes. We'll be recording the screen and audio — is that okay?"

"Before we start, can you tell me a bit about [relevant context — e.g., how you currently handle X]?"

## Tasks

### Task 1: [Name] (5-8 min)
**Scenario:** [Realistic context that motivates the task]
   Example: "You've just signed up for a new project management tool and want to create your first project for your marketing team."

**Goal:** [What success looks like — what you'll observe]
   Example: "User successfully creates a project and adds at least one team member."

**Steps to observe:**
- [ ] [Specific behavior to watch for]
- [ ] [Specific behavior to watch for]

**Probes (ask only after task completion):**
- "What did you expect to happen when you [action]?"
- "Was there anything confusing about that step?"
- "How would you describe what you just did in your own words?"

### Task 2: [Name] (5-8 min)
[Same structure as Task 1]

### Task 3: [Name] (5-8 min)
[Same structure as Task 1]

## Wrap-up (3 min)
- "Is there anything you'd change about what you saw today?"
- "On a scale of 1-7, how easy or difficult was it to [overall goal]?"
- "Any other feedback?"

## Post-session notes
[Fill in immediately after each participant]
- Task completion: [Which tasks succeeded/failed]
- Key observations: [Top 3-5 findings]
- Severity issues: [Critical / Major / Minor]
- Quotes: [2-3 memorable verbatim quotes]
```

## Moderation Techniques

### The Golden Rule

**You are testing the product, not the participant.** The participant never fails — the design fails them.

### Core Techniques

**Think-aloud protocol:**
- Ask participants to narrate their thought process as they work
- "Tell me what you're thinking as you look at this screen"
- "I noticed you paused there — what are you thinking about?"
- Don't interrupt flow to ask for narration

**The silence trick:**
- When a participant struggles, say nothing
- Count to 10 in your head
- They'll often figure it out or verbalize their confusion without prompting
- Only intervene if they're truly stuck and frustrated

**Probing without leading:**
- "What are you trying to do right now?" (not "Are you trying to find the settings?")
- "I see you looking at [area] — what are you thinking?" (not "Did you notice the button?")
- "Can you tell me more about that?" (not "Do you mean [specific thing]?")

** Minimal intervention:**
- Let participants struggle (within reason)
- Intervene only when they ask for help or become visibly frustrated
- If you help, note it as a failure of the design, not the participant

### Handling Common Situations

| Situation | Response |
|-----------|----------|
| Participant is stuck | "What would you do if I weren't here?" |
| Participant asks "Is this right?" | "What do you think?" or "There are no wrong answers." |
| Participant is frustrated | "That's really helpful feedback. Let's move on to the next task." |
| Participant speeds through | "Can you walk me through what you just did?" |
| Participant gives superficial feedback | "Can you give me a specific example?" |
| Participant is too polite | "What would you change if you could change one thing?" |

### What to Observe

Record these for each task:
- **Task success:** Did they complete it? (Yes / Partial / No / Gave up)
- **Time on task:** How long did it take?
- **Error rate:** How many wrong paths did they try?
- **Assist count:** How many times did you need to intervene?
- **Navigation path:** What route did they take?
- **Emotional response:** Frustration, surprise, delight, confusion
- **Verbalized expectations vs. reality:** "I thought this would do X, but it did Y"

## Remote Testing

### Moderated Remote (Preferred)

Best for: Qualitative insights, think-aloud, probing.

**Setup:**
- Video call tool (Zoom, Google Meet) with screen sharing
- Prototype on a shareable link (Figma, etc.)
- Record session (with permission)
- Have a note-taker (or AI notes tool) so moderator can focus on the participant

**Tips:**
- Ask participant to share their screen, not you sharing yours
- Request they close other apps and disable notifications
- Do a 2-minute tech check before starting
- Use chat to share prototype links rather than giving them ahead of time

### Unmoderated Remote

Best for: Quantitative validation, large sample sizes, when time is limited.

**Tools:** UserTesting, Maze, Lookback, Hotjar

**Trade-offs:**
- Pro: Scale, speed, lower cost per participant
- Con: No probing, no behavioral observation, harder to validate comprehension
- Use for: Task completion rates, time-on-task, click patterns
- Don't use for: First-time concept testing, complex flows, nuanced feedback

## Analysis and Reporting

### Post-Session Analysis

Immediately after each session:
1. **Log observations** while fresh (within 30 minutes)
2. **Tag findings** by type: critical issue, minor issue, insight, positive
3. **Rate severity** for each issue:

| Severity | Definition | Action |
|----------|------------|--------|
| **Critical** | User cannot complete task | Must fix before launch |
| **Major** | User struggles significantly, eventually completes | Should fix |
| **Minor** | User succeeds but with confusion or inefficiency | Consider fixing |
| **Cosmetic** | Small imperfection, no impact on task | Fix later |

### Cross-Session Synthesis

After all sessions, analyze patterns across participants:

1. **Affinity map observations** — Group similar findings across sessions
2. **Frequency analysis** — How many participants encountered each issue?
3. **Severity assessment** — Aggregate severity ratings across findings
4. **Create a findings matrix:**

| Finding | Freq (x/N) | Severity | Root Cause | Recommendation |
|---------|-----------|----------|------------|----------------|
| [Description] | 4/5 | Critical | [Why it happened] | [What to change] |

### Findings Report Template

```
# Usability Test Findings: [Feature/Product]

## Summary
[2-3 sentences: What was tested, with whom, and the top-level findings]

## Critical Findings
[Issues that block task completion. Fix before launch.]

## Major Findings
[Issues that cause significant friction. Fix soon.]

## Positive Findings
[What worked well. Protect these in future iterations.]

## Detailed Findings

### Finding 1: [Title]
- **Severity:** Critical / Major / Minor
- **Frequency:** X out of N participants
- **Evidence:** [Quote or behavioral observation]
- **Root cause:** [Why this happened]
- **Recommendation:** [Specific, actionable fix]

[Repeat for each finding]

## Next Steps
1. [Priority fix, assigned to, target date]
2. [Priority fix, assigned to, target date]
3. [Re-test timeline]
```

### Presenting Findings

- Lead with the headline: "4 out of 5 users couldn't find the checkout button"
- Show video clips of users struggling (1-2 short clips per critical finding)
- Use quotes, not paraphrases
- Connect every finding to a specific research question
- Prioritize ruthlessly — stakeholders can't process 50 findings. Lead with top 5.