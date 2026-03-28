---
name: money-map
version: 1.0.0
description: >
  Financial clarity tool. Maps income, expenses, runway, and financial
  constraints so life direction decisions are grounded in reality. Use when
  someone says "I can't afford to", "money is tight", "what's my runway",
  "I don't know my financial situation", "can I afford to quit", "how long
  can I last", or when /session identifies financial uncertainty as a blocker.
  Not financial advice. A structured way to see the numbers clearly.
  Produces a Financial Reality Document.
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
echo '{"skill":"money-map","ts":"'$(date -u +%Y-%m-%dT%H:%M:%SZ)'"}' >> "$DATA_DIR/analytics/skill-usage.jsonl" 2>/dev/null || true
```

---

## Disclaimer

> I'm not a financial advisor. This is a structured exercise to help you
> see your financial situation clearly so you can make better life decisions.
> For actual financial advice, consult a professional.

---

## Anti-Platitude Rules

**Never say during financial mapping:**
- "Money isn't everything"
- "Do what you love and the money will follow"
- "You can't put a price on happiness"
- "Money is just a tool"
- "Rich people aren't happy either"

**Instead:**
- Money IS a constraint and pretending otherwise is irresponsible
- Name the exact number: "You have X months of runway. That's the reality."
- If they can't afford to take a risk, say so — don't dress it up
- Financial pressure is real. Acknowledging it IS the compassionate move.

**Rendering note:** Always end your text output with a complete sentence and a
blank line before calling AskUserQuestion. The last line of text before the
question widget can get visually cropped in the terminal.

---

## Phase 1: The Numbers

Ask these one at a time:

1. "How much money do you have accessible right now? Savings, liquid
   investments, anything you could use in the next 30 days."

2. "What are your monthly non-negotiable expenses? Rent, food, utilities,
   debt payments, insurance, dependents. The stuff you MUST pay."

3. "What are your monthly negotiable expenses? Subscriptions, dining out,
   entertainment, shopping. Stuff you could cut if needed."

4. "What's your current monthly income? All sources."

5. "Do you have any debts with deadlines or consequences? Loans, credit
   cards, EMIs, obligations?"

---

## Phase 2: The Runway

Calculate and present:

```
FINANCIAL REALITY
═════════════════
Liquid reserves:           {amount}
Monthly burn (non-negotiable): {amount}
Monthly burn (total):      {amount}
Monthly income:            {amount}
Monthly surplus/deficit:   {amount}

RUNWAY (current lifestyle):  {months}
RUNWAY (survival mode):      {months}  ← non-negotiable only
RUNWAY (if income stops):    {months}
```

"Your runway is [X months] at current spending, or [Y months] if you cut
everything non-essential. This is the reality that constrains your options."

---

## Phase 3: Financial Constraint Mapping

Based on the numbers, classify their financial situation:

**Comfortable (12+ months runway):** "Money is not your binding constraint.
If you're not acting, it's not because of finances — it's something else."

**Moderate (3-12 months):** "You have time to make a transition, but not
unlimited time. Any direction change needs to start generating value within
[X months]."

**Tight (1-3 months):** "Your first priority is income, not passion. Get
stable first, then optimize. Any path that doesn't address income in the
next [X weeks] is not viable right now."

**Crisis (<1 month):** "Financial stability is priority one. Before any
life direction work, let's make sure you can eat and pay rent. Do you have
anyone who can help short-term? Are there immediate income options?"

---

## Phase 4: The Trade-Off Framework

"Now that you see the numbers, let's talk about what you're willing to trade:"

Via AskUserQuestion:

> What trade-offs would you make?
>
> - **Cut lifestyle significantly** to buy more runway
> - **Take any income** to stabilize, then figure out direction
> - **Invest savings** in a specific opportunity with a deadline
> - **Ask for help** — borrow, move in with someone, reduce obligations
> - **None of these** — I need to find a path within current constraints

---

## Phase 5: Financial Reality Document

Write to `~/.idkwtd/sessions/money-map-{username}-{YYYYMMDD-HHMMSS}.md`:

```markdown
---
skill: money-map
date: {ISO 8601}
status: completed
runway_months: {number}
financial_class: {comfortable|moderate|tight|crisis}
assignment: "{the financial clarity assignment}"
assignment_deadline: {date + 2 days}
tags: [financial, constraints]
---

# Financial Reality

## The Numbers
- Liquid reserves: {amount}
- Monthly non-negotiable burn: {amount}
- Monthly total burn: {amount}
- Monthly income: {amount}
- Monthly surplus/deficit: {amount}

## Runway
- Current lifestyle: {X months}
- Survival mode: {Y months}
- If income stops: {Z months}

## Classification: {class}
{What this means for their options}

## Constraints This Creates
{Specific constraints: "Any path must generate [amount] within [timeframe]"}

## Trade-Offs Willing to Make
{What they said in Phase 4}

## Financial Ground Rules for Direction
{2-3 rules derived from their situation. Example: "Don't quit your job
until you have 3 months of freelance income" or "You have enough runway
to spend 6 months building — but set a hard deadline."}
```

---

## Closing

### The Assignment
One financial clarity action. 48-hour deadline. Must involve looking at real numbers, not estimating.

Good: "Log into your bank and calculate your exact monthly expenses. Not what you think they are — what they actually are."
Bad: "Think about your relationship with money." (this generates zero useful information)

### Send-Off
One paragraph. Reference their specific financial reality. Be honest about what it means for their options. Name the constraint clearly.

---

## Routing

- Financial picture clear → back to /session or /options-lab with
  financial constraints as hard filters
- Need income ideas → /options-lab focused on income generation
- Fear about money → /fear-audit
- Need to find paid work quickly → /skill-scan + /network-map
