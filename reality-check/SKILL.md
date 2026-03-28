---
name: reality-check
version: 1.0.0
description: >
  Quick 5-minute gut check on a specific decision. Standalone skill, no prior
  session required. Use when someone says "should I do X", "is this a good
  idea", "I'm about to make a decision", "quick gut check", "reality check",
  "am I being stupid", "talk me out of this", "talk me into this", or any
  request for a fast assessment of a specific choice. Does not replace /session
  for complex situations. Produces a Go/No-Go Assessment.
allowed-tools:
  - Bash
  - Read
  - Write
  - AskUserQuestion
---

## Preamble

```bash
DATA_DIR="$HOME/.idkwtd"
mkdir -p "$DATA_DIR"/{sessions,analytics}
_TEL_START=$(date +%s)
echo '{"skill":"reality-check","ts":"'$(date -u +%Y-%m-%dT%H:%M:%SZ)'"}' >> "$DATA_DIR/analytics/skill-usage.jsonl" 2>/dev/null || true
```

---

## The Five-Minute Protocol

This skill is FAST. Five questions, one assessment. No long diagnostic.

### Q1: The Decision

"What's the specific decision? State it as clearly as you can in one sentence."

### Q2: The Reversibility Test

Via AskUserQuestion:

> How reversible is this decision?
>
> - **Fully reversible** — I can undo it easily (changing a job within same
>   field, trying a new side project, moving to a new apartment)
> - **Partially reversible** — I can undo it but with some cost (quitting a
>   job, ending a lease, dropping out of a program)
> - **Mostly irreversible** — very hard to undo (moving countries, having a
>   child, major financial commitment, burning a bridge)

### Q3: The Regret Test

"Imagine you're 80 years old looking back. Which would you regret more:
doing this and it not working out, or NOT doing this and never knowing?"

### Q4: The Body Check

"When you imagine yourself having already made this decision — right now,
picture it done — does your body feel relief or dread? Don't think about it.
What's the FIRST feeling?"

### Q5: The Advisor Test

"If your best friend described this exact situation to you, what would you
tell them to do?"

---

## Assessment

After the five questions, deliver the assessment:

```
REALITY CHECK: [Decision in one sentence]

REVERSIBILITY: [High/Medium/Low]
REGRET RISK:   [Higher if you do it / Higher if you don't]
GUT SIGNAL:    [Relief / Dread / Mixed]
YOUR OWN ADVICE: [What they said they'd tell a friend]

ASSESSMENT: [One paragraph. Direct. Name what you see.]

VERDICT: [GO / NO-GO / GO BUT WITH GUARDRAILS / NOT READY — NEED MORE INFO]
```

**If GO:** "Do it. Here's the first step: [concrete action, tomorrow]."

**If NO-GO:** "Don't do it. Here's why: [specific reason]. What you actually
want might be [alternative]."

**If GO WITH GUARDRAILS:** "Do it, but set these boundaries first: [1-2 specific
guardrails]. Example: 'Take the job but negotiate a 3-month review point.'"

**If NOT READY:** "You don't have enough information to decide yet. Here's the
one thing you need to find out first: [specific information gap]. Consider
running /session for a deeper diagnostic."

---

## Save Assessment

Write to `~/.idkwtd/sessions/reality-check-{username}-{YYYYMMDD-HHMMSS}.md`:

```markdown
---
skill: reality-check
date: {ISO 8601}
status: completed
decision: "{the decision}"
verdict: {go|no-go|go-with-guardrails|not-ready}
tags: [{tags}]
---

# Reality Check: {decision}

{Full assessment as above}
```

---

## Routing

If the person needs deeper exploration:
- Complex situation → /session
- Fear is the blocker → /fear-audit
- Financial uncertainty → /money-map
- Need to evaluate multiple options → /options-lab
