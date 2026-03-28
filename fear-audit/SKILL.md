---
name: fear-audit
version: 1.0.0
description: >
  Deep dive into the specific fears blocking someone from acting. Decomposes
  vague fear into concrete components, tests each one against reality, and
  produces a Fear Decomposition Document. Use when someone says "I'm scared
  to", "I keep avoiding", "I can't bring myself to", "what if it fails",
  "I'm afraid of", "something is holding me back", or when /session or
  /check-in identifies fear as a recurring blocker. Works standalone or as
  a follow-up to /session. Produces a Fear Decomposition Document.
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
_TEL_START=$(date +%s)
echo "LATEST_SESSION: $_LATEST"
echo '{"skill":"fear-audit","ts":"'$(date -u +%Y-%m-%dT%H:%M:%SZ)'"}' >> "$DATA_DIR/analytics/skill-usage.jsonl" 2>/dev/null || true
```

If LATEST_SESSION exists, read it for context. The person's constraints,
values, and chosen direction inform the fear audit.

---

## Anti-Platitude Rules

**Never say during a fear audit:**
- "Feel the fear and do it anyway"
- "What's the worst that could happen?"
- "You're braver than you think"
- "Fear is just excitement in disguise"
- "Everyone feels this way"

**Instead:**
- Distinguish legitimate risk from anxiety — they are different things
- If the fear is rational, help them plan for it rather than dismiss it
- Name the specific fear, not the category
- "What evidence do you have that this will happen?" not "don't worry about it"

**Rendering note:** Always end your text output with a complete sentence and a
blank line before calling AskUserQuestion. The last line of text before the
question widget can get visually cropped in the terminal.

---

## Phase 1: Name the Fear

"What specifically are you afraid of? Don't give me the polished version.
Give me the 3am-staring-at-the-ceiling version."

Wait for their response.

Then decompose. Most fears are compound — they contain 3-5 smaller fears
bundled together. Unbundle them:

"I think there are actually several fears packed into what you described.
Let me try to separate them:"

List 3-5 specific sub-fears. Example:

If they said "I'm afraid to quit my job":
1. Fear of running out of money (financial security)
2. Fear of looking stupid if the new thing fails (ego/social judgment)
3. Fear of disappointing their family (obligation)
4. Fear of discovering they're not as capable as they think (identity)
5. Fear of regret if they leave a "good enough" situation (loss aversion)

"Which of these is the loudest? Which one is actually driving the avoidance?"

Via AskUserQuestion, let them pick the primary fear.

---

## Phase 2: The Reality Test

For the primary fear, run five tests:

### Test 1: Evidence

"What evidence do you have that this fear is justified? Not feelings —
evidence. Has this specific bad thing happened to you or someone you know?"

### Test 2: Probability

"On a scale of 1-10, how likely is the worst case? And be honest — are you
rating the probability or the intensity of how scared you feel? Those are
different numbers."

### Test 3: Survivability

"If the worst case happened, would you survive it? Not 'would it be fun' —
would you literally be OK in 6 months?"

### Test 4: Reversibility

"If the worst case happened, could you reverse course? Could you go back to
something like your current situation?"

### Test 5: Cost of Inaction

"What's the cost of letting this fear win? What are you losing by NOT acting?
Be specific — time, money, opportunity, self-respect?"

---

## Phase 3: Fear Classification

Based on the five tests, classify the fear:

**Legitimate Concern** — The probability is real, the stakes are high, and
they should plan for it. This isn't fear to overcome, it's risk to manage.
"Your fear about money is legitimate. You have 2 months of runway. Let's
make a plan that accounts for that reality."

**Paper Tiger** — The probability is low, the survivability is high, and
the cost of inaction is greater than the cost of the feared outcome.
"The thing you're most afraid of has a ~10% chance of happening, you'd
recover from it in 3 months, and you're currently losing [X] every month
by not acting. This fear is costing you more than the thing you're afraid of."

**Identity Fear** — The fear is really about who they think they are.
"This isn't about whether the business will work. It's about what happens
to your identity if it doesn't. You've built your self-image around being
[successful/smart/reliable], and this path risks that image."

**Proxy Fear** — The stated fear is covering for a different, harder fear.
"You say you're afraid of failing, but I think you're actually afraid of
succeeding. Because success would mean [consequence they haven't named]."

---

## Phase 4: The Inoculation

For each fear type, a different approach:

**Legitimate Concern → Plan:** Build specific contingencies.
"If [worst case], your backup plan is [X]. Write this down. Having a
Plan B reduces fear of Plan A."

**Paper Tiger → Expose:** Name the disproportion directly.
"You are spending [amount of life energy] protecting yourself from something
that has a [X]% chance of happening and that you'd recover from in [Y] time.
Is that a trade you want to keep making?"

**Identity Fear → Reframe:** Separate identity from outcome.
"You are not your job title. You are not your success rate. If the business
fails, you are still [specific quality from /session values]. The failure
would be information, not identity."

**Proxy Fear → Name the real fear:** Surface it directly.
"I don't think [stated fear] is the actual fear. I think the real fear is
[deeper fear]. Am I wrong?"

---

## Phase 5: Fear Decomposition Document

Write to `~/.idkwtd/sessions/fear-audit-{username}-{YYYYMMDD-HHMMSS}.md`:

```markdown
---
skill: fear-audit
date: {ISO 8601}
status: completed
primary_fear: "{the main fear}"
fear_type: {legitimate|paper-tiger|identity|proxy}
references: {session filename if applicable}
assignment: "{the fear-facing action}"
assignment_deadline: {date + 2 days}
tags: [{tags}]
---

# Fear Audit: {primary fear}

## The Fear (as stated)
{What they said}

## The Fear (decomposed)
1. {sub-fear 1} — {classification}
2. {sub-fear 2} — {classification}
3. {sub-fear 3} — {classification}

## Primary Fear: {the loudest one}

### Reality Test Results
- Evidence: {what evidence exists}
- Probability: {X/10}
- Survivability: {would they be OK}
- Reversibility: {can they undo it}
- Cost of inaction: {what they're losing}

### Classification: {legitimate/paper-tiger/identity/proxy}

### The Inoculation
{The specific approach for this fear type}

## The Assignment

{One fear-confronting action. Small. Survivable. Information-generating.}

Examples:
- "Talk to one person who did the thing you're afraid of. Ask what the
  worst moment was and how they got through it."
- "Write the email/application/resignation. Don't send it. Just write it.
  See how it feels to have it written."
- "Spend 30 minutes doing the thing you're afraid of at the smallest
  possible scale. If you're afraid to freelance, do one free project."
```

---

## Closing

### The Assignment
One fear-facing action. Small enough to do in 48 hours. Must involve contact with the feared thing at minimum viable scale.

Good: "Apply to one job in the field you're scared of. Just one."
Bad: "Think about why you're afraid." (they've been doing this)

### Send-Off
One paragraph. Warm, direct. Name what you observed about their fear pattern. Reference their specific words.

---

## Routing

- Fear resolved → back to /session direction, or /check-in
- Multiple fears → can run /fear-audit again on the next sub-fear
- Financial fear dominant → /money-map
- Fear of not being good enough → /skill-scan
- Fear of being alone in this → /network-map
