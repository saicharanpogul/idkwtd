---
name: options-lab
version: 1.0.0
description: >
  Structured brainstorming and stress-testing of options. Use when someone
  has a problem space but needs to generate and evaluate options systematically.
  "Help me brainstorm", "what are my options", "I need ideas", "let's explore
  possibilities", "stress test this idea", "is this viable", or when /session
  Phase 4 needs deeper option analysis. Works standalone or after /session.
  Produces an Options Matrix document.
allowed-tools:
  - Bash
  - Read
  - Write
  - AskUserQuestion
  - WebSearch
---

## Preamble

```bash
DATA_DIR="$HOME/.idkwtd"
mkdir -p "$DATA_DIR"/{sessions,analytics}
_LATEST=$(ls -t "$DATA_DIR/sessions"/session-*.md 2>/dev/null | head -1 || echo "")
_SKILL_SCAN=$(ls -t "$DATA_DIR/sessions"/skill-scan-*.md 2>/dev/null | head -1 || echo "")
_MONEY_MAP=$(ls -t "$DATA_DIR/sessions"/money-map-*.md 2>/dev/null | head -1 || echo "")
echo "LATEST_SESSION: $_LATEST"
echo "SKILL_SCAN: $_SKILL_SCAN"
echo "MONEY_MAP: $_MONEY_MAP"
echo '{"skill":"options-lab","ts":"'$(date -u +%Y-%m-%dT%H:%M:%SZ)'"}' >> "$DATA_DIR/analytics/skill-usage.jsonl" 2>/dev/null || true
```

If prior sessions exist, read them for constraints, values, and skills.
This information filters options before they're generated.

---

## Phase 1: Problem Space

"What's the problem you need options for? Not a solution — the problem."

Then: "What constraints should I filter by?" Pull from prior sessions if
available, or ask directly.

---

## Phase 2: Diverge (Generate)

Generate 7-10 raw options. Go wide. Include:
- 2-3 obvious/conventional options
- 2-3 adjacent/creative options
- 1-2 radical/lateral options
- 1 "do nothing" option (always include this as a baseline)

For each: one sentence description. No evaluation yet.

Present the list. Ask: "Any of these spark something? Any I should add?
Any obviously wrong?"

Remove obvious misses. Add their additions.

---

## Phase 3: Converge (Filter)

Apply constraints as filters (from /session, /money-map, or stated now):
- Time constraint → eliminate options that take too long
- Money constraint → eliminate options that cost too much
- Skills constraint → eliminate options requiring skills they don't have
  (reference /skill-scan if available)
- Values constraint → eliminate options misaligned with values

After filtering, 3-5 options should remain.

---

## Phase 4: Stress Test

For each remaining option, run five tests:

1. **The 10/10/10 Test:** How will you feel about this in 10 minutes?
   10 months? 10 years?
2. **The Pre-Mortem:** Imagine this option failed. What's the most likely
   reason it failed?
3. **The Energy Test:** Does thinking about executing this option give you
   energy or drain you?
4. **The Dependency Test:** How many things outside your control need to
   go right for this to work?
5. **The Minimum Viable Test:** What's the smallest possible version of
   this you could test in one week?

---

## Phase 5: Options Matrix

Write to `~/.idkwtd/sessions/options-lab-{username}-{YYYYMMDD-HHMMSS}.md`:

```markdown
---
skill: options-lab
date: {ISO 8601}
status: completed
problem: "{the problem space}"
top_option: "{highest-scoring option}"
references: {prior session files}
tags: [{tags}]
---

# Options Lab: {problem space}

## Problem
{What they're solving for}

## Constraints Applied
{List of constraints used to filter}

## Options Matrix

| Option | Feasibility | Energy | Dependencies | Min Viable Test | Score |
|--------|------------|--------|-------------|----------------|-------|
| {opt}  | H/M/L      | H/M/L  | H/M/L       | {1-line test}  | {/15} |

## Top 3 Deep Dives

### Option 1: {name}
- Pre-mortem: {most likely failure mode}
- 10/10/10: {time horizon assessment}
- Minimum viable test: {what to do this week}

### Option 2: {name}
...

### Option 3: {name}
...

## Recommendation
{Which option to test first and why}

## The "Do Nothing" Baseline
{What happens if they choose none of these — the cost of inaction}
```

---

## Routing

- Ready to commit → back to /session for full Direction Document
- Need skills assessment for an option → /skill-scan
- Need financial viability check → /money-map
- Fear about top option → /fear-audit
- Need connections to execute → /network-map
