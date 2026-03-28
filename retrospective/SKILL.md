---
name: retrospective
version: 1.0.0
description: >
  Post-sprint retrospective. Run after completing a 14-day sprint from
  /session. Structured reflection: what worked, what didn't, what surprised
  you, what's next. Feeds back into /session for the next cycle. Use when
  someone says "I finished my sprint", "14 days are up", "retrospective",
  "what now", or has completed a Direction Document sprint.
allowed-tools:
  - Bash
  - Read
  - Write
  - AskUserQuestion
---

## Preamble

```bash
IDKWTD_ROOT=$(dirname "$(dirname "$(readlink -f "${BASH_SOURCE[0]}" 2>/dev/null || echo "$0")")" 2>/dev/null)
[ -z "$IDKWTD_ROOT" ] && IDKWTD_ROOT="$HOME/.claude/skills/idkwtd"
DATA_DIR="$HOME/.idkwtd"
mkdir -p "$DATA_DIR"/{sessions,analytics}
_LATEST_SESSION=$("$IDKWTD_ROOT/bin/idkwtd-sessions" latest-session 2>/dev/null || echo "")
_JOURNAL_COUNT=$(ls "$DATA_DIR/sessions/journal-"*.md 2>/dev/null | wc -l | tr -d ' ')
_TEL_START=$(date +%s)
echo "LATEST_SESSION: $_LATEST_SESSION"
echo "JOURNAL_ENTRIES: $_JOURNAL_COUNT"
echo '{"skill":"retrospective","ts":"'$(date -u +%Y-%m-%dT%H:%M:%SZ)'"}' >> "$DATA_DIR/analytics/skill-usage.jsonl" 2>/dev/null || true
```

**If LATEST_SESSION exists:** Read it. Load the Direction Document, the chosen path, the 14-day sprint plan, the assignments, and the "How You'll Know It's Working" signals.

**If no session exists:** "A retrospective works best after a /session sprint. Want to start with /session instead?"

---

## Anti-Platitude Rules

**Never say during a retrospective:**
- "Every experience is a learning opportunity"
- "At least now you know"
- "Failure is just feedback"
- "You should be proud of yourself"
- "The journey matters more than the destination"

**Instead:**
- If the sprint failed, name WHY it failed — specifically
- If they didn't follow the plan, ask what they did instead and why
- "What did you learn" is only useful if followed by "and what will you do differently"
- Celebrate actions taken, not feelings felt

**Rendering note:** Always end your text output with a complete sentence and a
blank line before calling AskUserQuestion. The last line of text before the
question widget can get visually cropped in the terminal.

---

## Phase 1: The Data

Read journal entries from the sprint period if available. Then ask via AskUserQuestion:

> Your sprint was: {sprint summary from Direction Document}
> Your path was: {chosen path}
>
> Two questions:
> 1. **What actually happened?** Not the plan — what you actually did.
> 2. **Did the "working" signals show up?** {list the signals from the Direction Document}

---

## Phase 2: The Analysis

After their response, deliver:

### What Worked
List specific actions that generated results. Quote their words and journal entries where possible.

### What Didn't
Name what was planned but not executed, and why. Be direct. "You planned to message 5 people and messaged 1. The blocker you named was [X]."

### The Surprise
One thing that emerged that wasn't in the original plan. There's always something. If they say "nothing surprised me," push: "What did you expect to be hard that was easy? Or easy that was hard?"

### The Update
Has the direction changed? Is the chosen path still right? Present honestly:
- **Stay the course** — the signals are positive, keep going
- **Adjust** — the direction is right but the approach needs tweaking
- **Pivot** — the sprint generated information that points somewhere else
- **Pause** — something external changed and you need to reassess

Ask via AskUserQuestion: "Based on all this — stay the course, adjust, pivot, or pause?"

---

## Phase 3: The Next Cycle

Based on their answer:

**Stay the course:** Design the next 14-day sprint. Build on what worked. Remove what didn't.

**Adjust:** Identify the specific adjustment. New sprint with the adjusted approach.

**Pivot:** "The sprint worked — it told you this isn't the path. That's a win, not a failure." Recommend /session for a fresh diagnostic with the new information.

**Pause:** Acknowledge. Suggest /journal to stay connected without pressure. Set a date to revisit.

---

## Output

Write to `~/.idkwtd/sessions/retrospective-{username}-{YYYYMMDD-HHMMSS}.md`:

```markdown
---
skill: retrospective
date: {ISO 8601}
status: completed
sprint_outcome: {stay|adjust|pivot|pause}
original_session: {filename of the session being reviewed}
assignment: "{next assignment}"
assignment_deadline: {date + 2 days}
tags: [{relevant tags}]
---

# Sprint Retrospective

**Original Direction:** {from Direction Document}
**Chosen Path:** {path name}
**Sprint Period:** {start date} — {end date}

## What Happened
{Narrative of what they actually did}

## What Worked
{Specific actions and results}

## What Didn't Work
{What was planned but not done, and why}

## The Surprise
{Unexpected finding}

## Sprint Outcome: {Stay / Adjust / Pivot / Pause}

{Explanation and rationale}

## Next Sprint
{If staying/adjusting: the new 14-day plan}
{If pivoting: recommendation for /session}
{If pausing: /journal cadence and revisit date}

## Assignment
{One concrete action, 48-hour deadline}
```

---

## Closing

### The Assignment
One action for the next 48 hours based on the sprint outcome.

### Send-Off
One paragraph. Reference their specific journey — where they started (the original session), what they learned, and where they're heading. Be warm but honest.

### Routing
- Stay/Adjust → /check-in in 7 days
- Pivot → /session for fresh diagnostic
- Pause → /journal daily, /session when ready
- If financial uncertainty emerged → /money-map
- If fear blocked execution → /fear-audit

---

## Telemetry

```bash
_TEL_END=$(date +%s)
_TEL_DUR=$(( _TEL_END - _TEL_START ))
echo '{"skill":"retrospective","ts":"'$(date -u +%Y-%m-%dT%H:%M:%SZ)'","duration":"'$_TEL_DUR'","outcome":"OUTCOME"}' >> ~/.idkwtd/analytics/skill-usage.jsonl 2>/dev/null || true
```
