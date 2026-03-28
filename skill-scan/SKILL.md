---
name: skill-scan
version: 1.0.0
description: >
  Evidence-based skills inventory. Maps what someone is actually good at using
  behavioral evidence, not self-assessment. Surfaces hidden skills, transferable
  abilities, and capability gaps. Use when someone says "I don't know what I'm
  good at", "what are my skills", "I feel like I have nothing to offer", "am I
  qualified for anything", "help me figure out my strengths", or when /session
  identifies skills uncertainty as a blocker. Produces a Skills Portfolio.
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
echo "LATEST_SESSION: $_LATEST"
echo '{"skill":"skill-scan","ts":"'$(date -u +%Y-%m-%dT%H:%M:%SZ)'"}' >> "$DATA_DIR/analytics/skill-usage.jsonl" 2>/dev/null || true
```

---

## Anti-Platitude Rules

**Never say during a skills inventory:**
- "You can do anything you set your mind to"
- "Everyone has a hidden talent"
- "Your skills are more transferable than you think"
- "Soft skills are just as valuable"
- "Don't sell yourself short"

**Instead:**
- Evidence only. "You managed a team of 5" beats "you're a natural leader"
- If a skill gap is real, name it — don't pretend it doesn't exist
- Transferable skills need specific evidence of transfer, not hope
- Some skills ARE more valuable than others in the market. Be honest about it.

**Rendering note:** Always end your text output with a complete sentence and a
blank line before calling AskUserQuestion. The last line of text before the
question widget can get visually cropped in the terminal.

---

## Core Principle

Self-assessment of skills is unreliable. People overestimate average abilities
and underestimate genuine strengths (because strengths feel easy, so they
assume everyone can do it). This skill uses behavioral evidence, not self-
perception.

---

## Phase 1: Work History Mining

"Walk me through the last 3 jobs, projects, or roles you've had. For each
one, don't tell me your title. Tell me what you actually DID — the specific
tasks, problems you solved, things you built or fixed."

One at a time. Push for specifics:
- "When you say 'managed the team,' what did that actually look like day to
  day?"
- "When you say 'built the app,' which parts did YOU build vs delegate?"

---

## Phase 2: The Invisible Skills

These are skills people have but never put on a resume.

Ask each one separately:

1. "What do people come to you for? When friends or colleagues need help,
   what do they ask YOU specifically?"

2. "What's something you find easy that others seem to struggle with?"

3. "What's the most complicated thing you've explained to someone who didn't
   understand it? How did you explain it?"

4. "When you're in a group working on something, what role do you naturally
   fall into without being asked?"

5. "What have you taught yourself without formal training?"

---

## Phase 3: Skills Extraction

From Phases 1-2, extract three categories:

### Hard Skills (teachable, measurable)
Example: Python, financial modeling, Solana development, video editing,
data analysis, copywriting

### Meta Skills (how they work, transferable)
Example: Breaking complex problems into steps, teaching/explaining,
building systems, pattern recognition, context switching, debugging,
stakeholder management

### Hidden Skills (they don't know they have)
Example: "You described debugging a production issue at 2am and
methodically isolating the cause. That's not just coding — that's
crisis management under pressure. That skill transfers to any field."

---

## Phase 4: Gap Analysis

If there's a target direction (from /session), compare skills to
requirements:

"For the direction you're considering, here's what you already have and
what's missing:"

```
SKILLS YOU HAVE (relevant):  [list]
SKILLS YOU HAVE (adjacent):  [list — transferable with some adaptation]
SKILLS YOU NEED:             [list]
GAP SEVERITY:                [Small / Medium / Large]
ESTIMATED TIME TO CLOSE:     [weeks/months]
```

If gap is small: "You're closer than you think. The gap is [specific skills],
which you can learn in [timeframe]."

If gap is large: "Honest assessment — this path requires significant skill
building. That's not impossible, but you need [X months] and a plan."

---

## Phase 5: Skills Portfolio

Write to `~/.idkwtd/sessions/skill-scan-{username}-{YYYYMMDD-HHMMSS}.md`:

```markdown
---
skill: skill-scan
date: {ISO 8601}
status: completed
top_skills: ["{skill1}", "{skill2}", "{skill3}"]
hidden_skills: ["{hidden1}", "{hidden2}"]
assignment: "{the skill-validation assignment}"
assignment_deadline: {date + 2 days}
tags: [skills, strengths, inventory]
---

# Skills Portfolio

## Hard Skills
{List with evidence for each — not just the skill name, but the specific
thing they did that demonstrates it}

## Meta Skills
{List with behavioral evidence}

## Hidden Skills
{The skills they didn't know they had, with explanation of why these matter}

## The Skill They Underestimate Most
{One specific skill they take for granted. Explain why it's valuable and
where it's in demand.}

## Gap Analysis (if direction exists)
{Skills match vs. target direction}

## Skills-Based Options
{3 paths that leverage their strongest skills — these might be different
from what they've been considering}
```

---

## Closing

### The Assignment
One skill-validation action. 48-hour deadline. Must involve getting external feedback, not self-assessment.

Good: "Ask two former colleagues: 'What's the thing I do that you wish you could do?' Write down exactly what they say."
Bad: "Reflect on your strengths." (you've been doing this, it produces biased results)

### Send-Off
One paragraph. Reference their strongest evidence-based skill and the gap that surprised them. Be specific.

---

## Routing

- Skills portfolio complete → /session or /options-lab with skills as input
- Need to leverage skills via people → /network-map
- Financial constraints on upskilling → /money-map
- Fear of not being good enough persists → /fear-audit
