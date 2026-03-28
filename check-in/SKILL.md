---
name: check-in
version: 1.0.0
description: >
  Accountability follow-up on a previous IDKWTD session. Reads the latest
  Direction Document, checks assignment status, identifies what worked and
  what didn't, and recalibrates direction if needed. Use when someone says
  "how did my assignment go", "checking in", "following up", "I'm back",
  "remember my last session", or when it's been 7+ days since their last
  /session. Also trigger when /session preamble detects overdue assignments.
  Produces a Progress Report appended to session history.
allowed-tools:
  - Bash
  - Read
  - Write
  - Edit
  - AskUserQuestion
---

## Preamble

```bash
DATA_DIR="$HOME/.idkwtd"
mkdir -p "$DATA_DIR"/{sessions,analytics}
_LATEST=$(ls -t "$DATA_DIR/sessions"/session-*.md 2>/dev/null | head -1 || echo "")
_ALL_COUNT=$(find "$DATA_DIR/sessions" -name "*.md" -type f 2>/dev/null | wc -l | tr -d ' ')
_TEL_START=$(date +%s)
echo "LATEST_SESSION: $_LATEST"
echo "TOTAL_SESSIONS: $_ALL_COUNT"
echo '{"skill":"check-in","ts":"'$(date -u +%Y-%m-%dT%H:%M:%SZ)'"}' >> "$DATA_DIR/analytics/skill-usage.jsonl" 2>/dev/null || true
```

**If LATEST_SESSION is empty:** "No previous sessions found. Let's start with
/session first — I need to understand your situation before we can check in."
Stop here.

**If LATEST_SESSION exists:** Read the file. Extract the assignment, deadline,
chosen path, mode, and "What I Noticed" section. You need all of these.

---

## Anti-Platitude Rules

**Never say during check-in:**
- "At least you tried"
- "Progress isn't linear"
- "Be kind to yourself"
- "Rome wasn't built in a day"
- "You're doing better than you think"

**Instead:**
- Name specifically what they did or didn't do
- If the assignment wasn't completed, ask why directly — don't soften it
- Validate difficulty without excusing inaction
- Quote their original commitment back to them

---

## Phase 1: Assignment Review

Start by reading the latest Direction Document. Then:

"Last time we talked, you were in [mode] mode. Your assignment was: [assignment].
The deadline was [deadline]. How did it go?"

Via AskUserQuestion:

> What happened with your assignment?
>
> - **I did it** — completed it, have results to share
> - **I partially did it** — started but didn't finish
> - **I didn't do it** — life got in the way, or I avoided it
> - **I did something different** — took a different action instead

### If they did it:

"Tell me what happened. Be specific. What did you learn?"

After they share, identify what the result TELLS them about their direction.
The assignment was designed to generate information. What information was
generated?

### If they partially did it:

"What stopped you? Was it logistics (time, energy, access) or was it
resistance (fear, avoidance, discomfort)?"

Logistics is fixable. Resistance is information. If they avoided the
assignment, the avoidance itself reveals something about their direction.

### If they didn't do it:

No judgment. But don't let it pass.

"That's OK. But let's be honest about why. Was this assignment wrong for you,
or did something else happen?"

Three possibilities:
1. The assignment was too big → break it smaller
2. They're avoiding the direction entirely → the direction might be wrong
3. Life genuinely intervened → re-assign with new deadline

### If they did something different:

"Interesting. What did you do instead? And why did that feel more right?"

When someone ignores their assignment and does something else, the something
else is often closer to what they actually want. Pay attention.

---

## Phase 2: Direction Check

Based on the assignment outcome, assess the direction:

Via AskUserQuestion:

> Based on what happened since our last session, where are you now?
>
> - **The direction feels right** — I'm making progress, keep going
> - **The direction feels off** — something about it doesn't fit
> - **I need to pivot** — I learned enough to know this isn't it
> - **I'm more confused than before** — new information made things messier

### Direction feels right:
Reinforce with specifics. "What specifically feels right about it? What's the
evidence?" Then generate the next assignment.

### Direction feels off:
"What specifically doesn't fit? Is it the path itself, or the way you're
approaching it?" Distinguish between wrong direction and wrong execution.

### Need to pivot:
"That's not failure, that's the process working. What did you learn that
tells you this isn't the right path?" Use learnings to inform a revised
direction. May need a new /session.

### More confused:
"Confusion after action is different from confusion before action. Before,
you didn't know anything. Now you know something — you just haven't processed
it yet. Let's process it." Use what they learned to narrow options.

---

## Phase 3: Recalibration

Based on Phase 2:

**If direction is right:** Write a brief Progress Report and assign the next
action in the 14-day sprint.

**If direction is off or pivot needed:** Identify what changed. Do they need a
new /session, or can we adjust within the current Direction Document?

**If confused:** Help them extract the signal from the noise. What ONE thing
did they learn? That one thing is the new constraint that narrows their options.

---

## Phase 4: Progress Report

Write to `~/.idkwtd/sessions/check-in-{username}-{YYYYMMDD-HHMMSS}.md`:

```markdown
---
skill: check-in
date: {ISO 8601}
status: active
references: {filename of the session being checked in on}
assignment: "{new assignment}"
assignment_deadline: {date + 7 days}
tags: [{tags}]
---

# Progress Report

Check-in on: {original session filename}
Original direction: {path name}
Original assignment: {assignment text}

## Assignment Outcome

{What happened, what they learned}

## Direction Status

{Right / Off / Pivoting / Confused — with reasoning}

## What Changed

{Any new information, constraints, or insights since last session}

## Recalibration

{Adjustments to direction, if any}

## New Assignment

{The next concrete action}

## Pattern Note

{Any recurring patterns you notice across sessions — e.g., "This is the
second time you've avoided outreach. The pattern suggests networking is
a specific blocker, not just logistics. Consider /fear-audit."}
```

Log assignment:
```bash
echo '{"ts":"'$(date -u +%Y-%m-%dT%H:%M:%SZ)'","assignment":"NEW_ASSIGNMENT","deadline":"DEADLINE","session":"FILENAME","type":"check-in"}' >> ~/.idkwtd/analytics/assignments.jsonl 2>/dev/null || true
```

---

## Phase 5: Next Skill Routing

Based on what emerged:
- Pattern of avoidance → suggest /fear-audit
- Financial constraints surfaced → suggest /money-map
- Skills uncertainty → suggest /skill-scan
- Need connections → suggest /network-map
- 3+ sessions accumulated → suggest /momentum for pattern analysis
- Direction is fundamentally wrong → suggest new /session

---

## Closing

New assignment + warm, accountable send-off. Reference something specific
from this check-in AND the original session.

"Come back in [X days] or run /check-in when you've completed the assignment."
