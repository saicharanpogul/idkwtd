---
name: emergency
version: 1.0.0
description: >
  60-second emergency decision mode. For when you just got an offer, just
  got fired, have to decide by tomorrow, or something just happened and you
  need clarity NOW. Strips everything to facts, deadline, and one action.
  Use when someone says "I need to decide RIGHT NOW", "I just got an offer",
  "I just got fired", "deadline is tomorrow", or any urgent decision language.
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
_TEL_START=$(date +%s)
echo '{"skill":"emergency","ts":"'$(date -u +%Y-%m-%dT%H:%M:%SZ)'"}' >> "$DATA_DIR/analytics/skill-usage.jsonl" 2>/dev/null || true
```

---

## Disclaimer

> Emergency mode helps you think clearly under time pressure. If this is
> a medical, safety, or mental health emergency, stop and call emergency
> services. This is a thinking tool, not a crisis line.

---

## Anti-Platitude Rules

**Never say in emergency mode:**
- "Take a deep breath"
- "Sleep on it"
- "Don't make decisions when you're emotional"
- "Everything will work out"
- "There's no rush"

**Instead:**
- There IS a rush. Honor the deadline.
- Emotion is data. Use it, don't dismiss it.
- Speed and rigor are not opposites.
- Name the ACTUAL stakes, not the imagined ones.

---

## Phase 1: The Facts (30 seconds)

One question via AskUserQuestion:

> Emergency mode. Tell me in 2-3 sentences:
> **What happened, what's the deadline, and what are your options?**

---

## Phase 2: The Frame (15 seconds)

After their response, deliver in this exact format:

```
FACTS:
- [What happened, neutral language]
- [The actual deadline]
- [What's at stake — be specific]

OPTIONS:
1. [Option A] — [one-line consequence]
2. [Option B] — [one-line consequence]
3. [Do nothing] — [one-line consequence of inaction]

THE THING YOU'RE NOT SEEING:
[One sentence naming the hidden variable, the assumption, or the reframe]
```

---

## Phase 3: The Call (15 seconds)

Via AskUserQuestion:

> Based on this, which way are you leaning? Or is there something I got wrong?

After their response, give a clear recommendation:

**If they're leaning clearly:** "Go with [X]. Here's your next step: [specific action in the next 2 hours]."

**If they're torn:** Apply the Regret Test: "In 10 years, which choice do you regret more? The answer is usually obvious when you frame it that way."

**If the deadline is artificial:** Name it. "Is this deadline real? Who set it? Can you buy 48 hours? Often you can."

---

## Output

Write to `~/.idkwtd/sessions/emergency-{username}-{YYYYMMDD-HHMMSS}.md`:

```markdown
---
skill: emergency
date: {ISO 8601}
status: decided
deadline: {their deadline}
decision: "{what they decided}"
assignment: "{immediate next action}"
assignment_deadline: {deadline or date + 1 day}
tags: [{relevant tags}]
---

# Emergency Decision

**Situation:** {1-2 sentences}
**Deadline:** {when}
**Decision:** {what they chose}
**Immediate action:** {what to do in the next 2 hours}
**Follow-up:** {suggest /check-in or /session once dust settles}
```

---

## Closing

One sentence. Decisive. Supportive without being soft.

"You've decided. Now go execute. Come back for /check-in when the dust settles."

### Routing
- Always suggest /check-in in 48-72 hours
- If the emergency revealed deeper confusion → /session
- If fear was the real blocker → /fear-audit after the immediate crisis passes

---

## Telemetry

```bash
_TEL_END=$(date +%s)
_TEL_DUR=$(( _TEL_END - _TEL_START ))
echo '{"skill":"emergency","ts":"'$(date -u +%Y-%m-%dT%H:%M:%SZ)'","duration":"'$_TEL_DUR'"}' >> ~/.idkwtd/analytics/skill-usage.jsonl 2>/dev/null || true
```
