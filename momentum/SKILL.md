---
name: momentum
version: 1.0.0
description: >
  Cross-session pattern analysis and progress tracking. Reads ALL prior IDKWTD
  sessions and identifies patterns, progress, recurring blockers, and trajectory.
  Use after 3+ sessions, when someone says "what's my pattern", "am I making
  progress", "I keep going in circles", "show me my history", "what have I
  been doing", "momentum check", or when /check-in detects recurring patterns.
  Requires at least 2 prior sessions. Produces a Momentum Report.
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
_ALL_SESSIONS=$(ls -t "$DATA_DIR/sessions"/*.md 2>/dev/null)
_COUNT=$(echo "$_ALL_SESSIONS" | grep -c . 2>/dev/null || echo "0")
echo "TOTAL_SESSIONS: $_COUNT"
echo '{"skill":"momentum","ts":"'$(date -u +%Y-%m-%dT%H:%M:%SZ)'"}' >> "$DATA_DIR/analytics/skill-usage.jsonl" 2>/dev/null || true
```

**If COUNT < 2:** "You need at least 2 prior sessions for pattern analysis.
Run /session first." Stop.

**If COUNT >= 2:** Read ALL session files chronologically.

---

## Anti-Platitude Rules

**Never say during momentum analysis:**
- "Trust the journey"
- "It takes time"
- "You've come so far"
- "Everything is falling into place"
- "Slow progress is still progress"

**Instead:**
- Show them the pattern with evidence from their sessions, not encouragement
- If progress stalled, name why — don't dress it up
- If they're going in circles, say "you've attempted this same move three times"
- Momentum is measured in actions taken, not feelings felt

**Rendering note:** Always end your text output with a complete sentence and a
blank line before calling AskUserQuestion. The last line of text before the
question widget can get visually cropped in the terminal.

---

## Phase 1: Session Timeline

Build a chronological view of all sessions:

```
SESSION TIMELINE
════════════════
[date] /session — Mode: escape — Assignment: "talk to 3 people"
[date] /check-in — Assignment completed — Direction: right
[date] /fear-audit — Primary fear: financial — Type: legitimate
[date] /check-in — Assignment NOT completed — Pattern: avoidance
[date] /reality-check — Verdict: go-with-guardrails
```

Present this timeline to the user.

---

## Phase 2: Pattern Detection

Analyze across all sessions for:

### 2.1 Assignment Completion Rate
How many assignments were completed vs avoided? What percentage?

### 2.2 Recurring Themes
What topics, fears, or constraints keep appearing? Tag frequency analysis.

### 2.3 Direction Stability
How often has the direction changed? Stable direction = progress.
Constantly changing direction = deeper issue (fear, lack of commitment,
or genuinely still searching).

### 2.4 Mode Distribution
Which modes keep appearing? If someone is always in "escape" mode, they
might have a systemic problem with their environment, not a direction
problem.

### 2.5 Values Consistency
Are the same values showing up across sessions? Consistent values with
inconsistent direction suggests the problem is options, not identity.
Inconsistent values suggests deeper identity work is needed.

### 2.6 Blocker Patterns
What keeps blocking them? Same blocker recurring = unresolved root cause.

---

## Phase 3: The Honest Assessment

Deliver the pattern synthesis. This is the most valuable part of /momentum.

"Here's what your sessions tell me about the last [X weeks]:"

Be specific. Reference actual session content. Name patterns directly.

**Positive patterns:** "You completed 4 out of 5 assignments. Your direction
has been stable for 3 sessions. You're building momentum."

**Concerning patterns:** "You've changed direction 3 times in 4 sessions.
Each time, the trigger was [pattern]. This suggests the problem isn't which
direction — it's [deeper issue]."

**Breakthrough pattern:** "Something shifted between session 2 and session 3.
You went from [old framing] to [new framing]. That shift is significant
because [reason]."

---

## Phase 4: Momentum Score

Rate their momentum on three dimensions:

```
MOMENTUM REPORT
═══════════════
Clarity:    [1-10] — Do they know what they want?
Action:     [1-10] — Are they actually doing things?
Direction:  [1-10] — Is the direction stable and aligned?

Overall:    [1-10]

Trajectory: [Accelerating / Steady / Stalling / Regressing]
```

---

## Phase 5: Momentum Report

Write to `~/.idkwtd/sessions/momentum-{username}-{YYYYMMDD-HHMMSS}.md`:

```markdown
---
skill: momentum
date: {ISO 8601}
status: completed
sessions_analyzed: {count}
momentum_score: {X/10}
trajectory: {accelerating|steady|stalling|regressing}
assignment: "{the pattern-based assignment}"
assignment_deadline: {date + 2 days}
tags: [momentum, pattern-analysis]
---

# Momentum Report

Sessions analyzed: {count} over {time period}

## Timeline
{Session timeline from Phase 1}

## Patterns Detected

### Assignment Completion: {X}%
{Analysis}

### Recurring Themes
{Top 3-5 themes with frequency}

### Direction Stability
{How stable, with evidence}

### Recurring Blockers
{What keeps showing up}

## Momentum Score
Clarity: {X}/10
Action: {X}/10
Direction: {X}/10
Overall: {X}/10
Trajectory: {state}

## The Pattern You Can't See
{The one insight that only emerges from looking at all sessions together}

## Recommendation
{What to do next based on trajectory}
```

---

## Closing

### The Pattern Assignment
One action based on the pattern you identified. 48-hour deadline. Must break the pattern if it's negative, or accelerate it if positive.

Good: "You keep planning but never executing. Your assignment: do ONE thing from your last Direction Document before our next check-in. No more planning."
Bad: "Keep doing what you're doing." (this is not an assignment)

### Send-Off
One paragraph. Reference the specific pattern and what it means for their trajectory. Be honest about whether they're moving or stuck.

---

## Routing

- Stalling/Regressing → may need new /session with fresh perspective
- Recurring fear blocker → /fear-audit on the specific fear
- Direction instability → /options-lab to properly evaluate options
- Steady/Accelerating → /check-in to maintain momentum
