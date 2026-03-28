---
name: network-map
version: 1.0.0
description: >
  Maps existing relationships and identifies who can help with what. Turns
  "I don't know anyone" into a concrete list of people to contact and what
  to ask them. Use when someone says "I don't have connections", "I don't
  know who to talk to", "how do I network", "I need introductions", "who
  can help me", or when /session or /skill-scan identifies relationship
  leverage as a next step. Produces a Network Action Plan.
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
_SKILL_SCAN=$(ls -t "$DATA_DIR/sessions"/skill-scan-*.md 2>/dev/null | head -1 || echo "")
_LATEST=$(ls -t "$DATA_DIR/sessions"/session-*.md 2>/dev/null | head -1 || echo "")
echo "SKILL_SCAN: $_SKILL_SCAN"
echo "LATEST_SESSION: $_LATEST"
echo '{"skill":"network-map","ts":"'$(date -u +%Y-%m-%dT%H:%M:%SZ)'"}' >> "$DATA_DIR/analytics/skill-usage.jsonl" 2>/dev/null || true
```

If /skill-scan exists, read it for skills to leverage.
If /session exists, read it for direction and constraints.

---

## Core Insight

"I don't know anyone" is almost never true. What's true is "I don't know
anyone who can help with THIS SPECIFIC THING." The skill's job is to
surface people they already know but haven't thought of as resources.

---

## Phase 1: The People Inventory

"Let's map who you actually know. Don't filter for relevance yet. Just
list people."

Ask each one separately:

1. "Who are the 5 people you talk to most? Family, friends, anyone."

2. "Who do you know from previous jobs or projects? Names, even if you
   haven't talked in years."

3. "Who do you know who does something you find interesting? Even if you
   don't know them well."

4. "Who have you helped in the past? People who might owe you a favor or
   would be happy to hear from you."

5. "Who do you follow online whose work you respect? Even if you've never
   interacted."

---

## Phase 2: Relationship Classification

For each person mentioned, classify:

**Inner Circle** — Talk regularly, high trust, can ask for real help
**Warm Network** — Know them, positive relationship, could reconnect
**Cold Network** — Know of them, no relationship, would need introduction
**Aspirational** — Don't know them, but they're relevant to the direction

---

## Phase 3: Opportunity Matching

Cross-reference the people with the person's direction (from /session)
and skills (from /skill-scan).

For each relevant person, identify:
- What they could help with (information, introduction, opportunity, advice)
- What the ask would be (specific, not "can you help me")
- How to approach them (what to say, what to offer in return)

---

## Phase 4: The Three Conversations

Identify the three highest-value conversations:

```
CONVERSATION 1: {Name}
  Relationship: {inner circle / warm / cold}
  What they can help with: {specific thing}
  The ask: {exact message/question}
  Why now: {why this is the right time to reach out}

CONVERSATION 2: {Name}
  ...

CONVERSATION 3: {Name}
  ...
```

Rules for the ask:
- Be specific. Not "can I pick your brain" but "I'm exploring [X] and
  you've done [Y]. Could I ask you 2 questions about [Z]?"
- Offer value first if possible. "I noticed you're working on [X], I
  have experience with [Y] that might help."
- Make it easy to say yes. Short ask, specific time, low commitment.
- For cold/aspirational contacts: find a genuine connection point first.
  Never cold-email with just an ask.

---

## Phase 5: Network Action Plan

Write to `~/.idkwtd/sessions/network-map-{username}-{YYYYMMDD-HHMMSS}.md`:

```markdown
---
skill: network-map
date: {ISO 8601}
status: active
assignment: "{the three conversations}"
assignment_deadline: {date + 7 days}
tags: [network, relationships, outreach]
---

# Network Action Plan

## Direction Context
{What they're trying to do, from /session}

## People Map

### Inner Circle ({count})
{Names and what they could help with}

### Warm Network ({count})
{Names and opportunity}

### Cold Network ({count})
{Names and approach strategy}

### Aspirational ({count})
{Names and connection points}

## The Three Conversations

{Detailed conversation plans from Phase 4}

## Message Templates

### For Inner Circle
"Hey [name], I'm working on [specific thing]. You know about [specific
area]. Could I ask you [specific question]? Would take 10 minutes."

### For Warm Network (reconnecting)
"Hey [name], it's been a while. I saw you're doing [thing]. That's
great. I'm exploring [direction] and thought of you because [specific
reason]. Any chance we could talk for 15 minutes this week?"

### For Cold Network
{Approach depends heavily on context — provide specific template}

## The Anti-Networking Rule
Don't "network." Have genuine conversations. Ask real questions. Be
interested in them, not just what they can do for you. The best
professional relationships start as human ones.
```

---

## Assignment

"Your assignment: have these three conversations within 7 days. Come back
and run /check-in to tell me what you learned."

---

## Routing

- Conversations happened → /check-in
- Fear of reaching out → /fear-audit
- Need to know what to talk about → /skill-scan
- Need financial context for the ask → /money-map
