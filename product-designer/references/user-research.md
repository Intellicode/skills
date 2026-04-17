# User Research

## Table of Contents

- [Research Methods](#research-methods)
- [Interview Guide](#interview-guide)
- [Survey Design](#survey-design)
- [Synthesis Techniques](#synthesis-techniques)
- [Research Plan Template](#research-plan-template)

## Research Methods

Choose methods based on what you need to learn and project constraints:

| Method | Best For | Time | Participants |
|--------|----------|------|-------------|
| User interviews | Deep understanding of needs, motivations, behaviors | 45-60 min each | 5-8 per segment |
| Contextual inquiry | Understanding workflows in natural environment | 1-2 hours each | 4-6 |
| Diary study | Behavior over time, habit formation | 1-2 weeks | 10-20 |
| Survey | Quantifying patterns, prioritizing needs, large-sample validation | 10-15 min | 100+ |
| Usability test | Evaluating existing solutions, identifying friction | 30-60 min each | 5-8 |
| Card sorting | Information architecture, content organization | 15-30 min each | 15-20 |
| Tree testing | Validating navigation structure | 5-10 min each | 20-50 |

### When to Use Each Method

**Explore a new problem space:** Interviews → Survey → Card sort
**Improve an existing product:** Usability test → Survey → Interviews
**Understand long-term behavior:** Diary study → Interviews
**Restructure navigation/content:** Card sort → Tree test → Usability test

## Interview Guide

### Structure

A good interview guide has 3 sections:

1. **Warmup (5 min)** — Establish rapport. Easy, non-threatening questions.
2. **Core (30-40 min)** — Explore the topic area. Follow the thread, not the script.
3. **Wrap-up (5 min)** — Summary questions. Ask what you missed.

### Interview Principles

- Ask about **past behavior**, not future intent. "Tell me about the last time you..." not "Would you use...?"
- Use **open-ended questions**. Avoid yes/no questions.
- **Don't lead.** Replace "Do you find it frustrating when..." with "How does that feel?" 
- **Silo questions.** Ask one thing at a time.
- **The 5-second rule.** After the participant finishes speaking, wait. They often add the most valuable detail in that pause.
- **Paraphrase and confirm.** "So what I'm hearing is..." ensures understanding and builds trust.

### Question Templates

| Purpose | Template | Example |
|---------|----------|---------|
| Open exploration | "Tell me about the last time you [action]" | "Tell me about the last time you booked a flight" |
| Specific detail | "Walk me through how you [process]" | "Walk me through how you onboard a new client" |
| Emotional context | "How did you feel when [event]" | "How did you feel when the payment failed?" |
| Priority | "What's the hardest part about [activity]" | "What's the hardest part about managing your team?" |
| Alternatives | "What have you tried to solve [problem]" | "What have you tried to solve the scheduling conflict?" |
| Gaps | "Is there anything else about [topic] I should know?" | "Is there anything else about your workflow I should know?" |

### Anti-patterns to Avoid

- "Don't you think that..." (leading)
- "Would you use a feature that..." (hypothetical)
- "Do you like X or Y?" (forced choice without context)
- "Why didn't you just..." (implied criticism)

## Survey Design

### When Surveys Work

- Quantifying what you discovered in interviews
- Prioritizing features or pain points across a large audience
- Tracking attitudes or behaviors over time
- Segmenting your user base

### Survey Structure

1. **Screening (2-3 questions)** — Ensure respondent is in your target audience
2. **Core (8-12 questions)** — The questions that answer your research goals
3. **Demographics (3-4 questions)** — Context variables for analysis
4. **Open-ended (1-2 questions)** — Catch anything you missed

### Question Types

| Type | Use For | Example |
|------|---------|---------|
| Likert scale | Attitude Strength | "How important is [feature]?" (1-5) |
| Multiple choice | Segmentation | "Which best describes your role?" |
| Rank order | Prioritization | "Rank these features by importance" |
| Matrix | Compare items | Rate multiple features on same scale |
| Open text | Discovery | "What's your biggest challenge with [topic]?" |

### Survey Pitfalls

- **Double-barreled questions:** "How satisfied are you with the speed and reliability?" → Split into two questions
- **Leading language:** "How much do you love our new feature?" → "How would you rate our new feature?"
- **Acquiescence bias:** People agree with statements. Use both positive and negative framings.
- **Too long:** Max 15 minutes. Response quality drops after ~10 questions.

## Synthesis Techniques

### Affinity Mapping

Group observations to find themes. Best after interviews or open-ended research.

1. Write each observation on a separate note (one insight per note)
2. Read all notes silently
3. Sort notes into clusters without talking (silent sorting)
4. Name each cluster with the theme it represents
5. Review clusters for hierarchy — some clusters combine into overarching themes

### Empathy Map

Capture what a user persona thinks, feels, says, and does. Use after interviews to make a persona tangible.

| Quadrant | Questions |
|----------|-----------|
| **Says** | What did you hear them say directly? Quotes, opinions, attitudes. |
| **Thinks** | What might they think but not say? Concerns, preoccupations, aspirations. |
| **Does** | What actions and behaviors did you observe? What steps do they take? |
| **Feels** | What emotions came through? Frustrations, delights, anxieties. |

Add a bottom section for:
- **Pains** — Negative emotions, risks, obstacles
- **Gains** — Positive outcomes, wants, success measures

### Persona Framework

Build personas from research data, not assumptions. Each persona needs:

- **Name and photo** — Makes them memorable
- **Demographics** — Role, experience level, context
- **Goals** — What they're trying to accomplish
- **Behaviors** — How they currently solve the problem
- **Pain points** — Where they struggle most
- **Quote** — A representative verbatim quote from interviews

Validate: Does each persona have at least 3 supporting data points from research?

### Journey Map

Map the user's end-to-end experience through a process.

| Stage | Actions | Thoughts | Feelings | Pain Points | Opportunities |
|-------|---------|----------|----------|-------------|---------------|
| [Stage 1] | What they do | What they think | Emotions (😊😐😫) | Frictions | Design ideas |

Key principles:
- Base on research, not assumptions
- Include emotional highs and lows
- Identify handoffs between channels or systems
- Focus on pain points — they're the design opportunities

## Research Plan Template

```
# Research Plan: [Project Name]

## Background
[1-2 sentences on why this research matters now]

## Objectives
[What you need to learn. 2-4 specific, answerable questions.]

## Method
[Which method(s) and why they're appropriate]

## Participants
- Target: [Who]
- Recruiting: [How]
- Sample size: [N]
- Screener criteria: [Must have / Must not have]

## Timeline
| Activity | Date |
|----------|------|
| Research plan approved | [Date] |
| Recruitment complete | [Date] |
| Sessions conducted | [Date range] |
| Analysis complete | [Date] |
| Findings presented | [Date] |

## Discussion Guide / Survey
[Link to interview guide or full survey]

## Analysis Plan
[How findings will be synthesized: affinity mapping, thematic analysis, statistical analysis, etc.]

## Deliverables
[What comes out: personas, journey map, report, presentation, etc.]
```

### Participant Recruitment Tips

- 5 participants uncover 85% of usability problems (Nielsen)
- 8-12 interviews achieve thematic saturation for qualitative research
- Recruit from actual or potential users, not friends/colleagues
- Offer fair compensation (typically $50-150/session depending on audience)
- Over-recruit by 20% to account for no-shows