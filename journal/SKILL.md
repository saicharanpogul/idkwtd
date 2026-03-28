---
name: journal
version: 1.0.0
description: >
  Quick daily direction journal. 2 minutes. Three questions that build the
  data /momentum uses for pattern analysis. Use when someone says "just
  checking in", "daily log", "quick update", or wants to track progress
  without a full session. Designed for daily use between sessions.
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
_LATEST=$("$IDKWTD_ROOT/bin/idkwtd-sessions" latest 2>/dev/null || echo "")
_TEL_START=$(date +%s)
echo '{"skill":"journal","ts":"'$(date -u +%Y-%m-%dT%H:%M:%SZ)'"}' >> "$DATA_DIR/analytics/skill-usage.jsonl" 2>/dev/null || true
```

If a latest session exists, read it silently for context. Don't mention it unless relevant.

---

## Anti-Platitude Rules

**Never say in a journal entry:**
- "Every day is a fresh start"
- "You're making progress just by showing up"
- "Be grateful for what you have"
- "Tomorrow is another day"

**Instead:**
- If they did nothing, say "you did nothing today — that's data, not a judgment"
- If they're stuck in the same pattern, name it
- Keep it fast. This is a 2-minute tool, not therapy.

---

## The Three Questions

Ask all three via a single AskUserQuestion:

> Quick journal. Three things:
>
> 1. **What did you do today** toward your direction? (Even tiny counts. "Nothing" is an honest answer.)
> 2. **What got in the way?** (External blocker, internal resistance, or just life?)
> 3. **Energy level right now?** (1-10, gut feeling)

---

## Processing

After their response:

- If they did something: acknowledge it in ONE sentence. No cheerleading.
- If they did nothing: "Noted. That's [X] days with no action." (count from recent journals if available). No judgment, just the number.
- If a blocker is recurring: "This is the [Nth] time [blocker] has come up. Worth looking at."
- If energy is consistently low (3+ entries below 5): "Your energy has been low for [N] days. That's a signal worth paying attention to."

Do NOT give advice. Do NOT generate options. This is a log, not a session.

---

## Output

Write to `~/.idkwtd/sessions/journal-{username}-{YYYYMMDD-HHMMSS}.md`:

```markdown
---
skill: journal
date: {ISO 8601}
status: logged
energy: {1-10}
action_taken: {yes|no}
blocker: "{blocker or none}"
tags: [{relevant tags}]
---

# Journal Entry

**Action:** {what they did or "none"}
**Blocker:** {what got in the way or "none"}
**Energy:** {N}/10
**Pattern note:** {any pattern you noticed, or "—"}
```

---

## Closing

One sentence max. Examples:
- "Logged. See you tomorrow."
- "Three days, no action. Something's in the way. Consider /fear-audit."
- "Logged. Energy trending down — watch that."

### Routing (only if patterns warrant it)
- 5+ days no action → suggest /fear-audit
- Energy below 5 for a week → suggest checking in with themselves (not IDKWTD — this might be health)
- 7+ journal entries → suggest /momentum for pattern analysis
- No prior /session → suggest /session

---

## Telemetry

```bash
_TEL_END=$(date +%s)
_TEL_DUR=$(( _TEL_END - _TEL_START ))
echo '{"skill":"journal","ts":"'$(date -u +%Y-%m-%dT%H:%M:%SZ)'","duration":"'$_TEL_DUR'"}' >> ~/.idkwtd/analytics/skill-usage.jsonl 2>/dev/null || true
```
