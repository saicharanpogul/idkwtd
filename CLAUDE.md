# IDKWTD — I Don't Know What To Do

Life direction skill stack. 9 interconnected skills for helping people
who feel stuck find their next move.

## Available Skills

- `/session` — Full life direction diagnostic. Entry point. 40-60 min.
  Use when someone says "I don't know what to do", "I feel stuck", "I feel
  lost", "help me figure things out", or any variation of life uncertainty.

- `/check-in` — Accountability follow-up. Reads the latest Direction
  Document, checks assignment status. 15 min.

- `/reality-check` — Quick 5-minute gut check on a specific decision.
  Standalone, no prior session needed.

- `/fear-audit` — Deep dive into what's blocking action. Decomposes fear
  into components, classifies, and provides targeted inoculation. 20 min.

- `/options-lab` — Structured brainstorming. Generate, filter, and
  stress-test options. 20 min.

- `/momentum` — Cross-session pattern analysis. Reads ALL prior sessions.
  Requires 2+ prior sessions. 10 min.

- `/money-map` — Financial clarity. Maps income, expenses, runway. Not
  financial advice. 15 min.

- `/skill-scan` — Evidence-based skills inventory using behavioral
  evidence, not self-assessment. 15 min.

- `/network-map` — Maps existing relationships and identifies who can
  help with what. 15 min.

## Data

All sessions write to `~/.idkwtd/sessions/` with YAML frontmatter.
Skills read each other's output for cross-session context.
Analytics in `~/.idkwtd/analytics/`.

## Key Files

- `ETHOS.md` — 8 philosophical principles. Read before modifying skills.
- `ARCHITECTURE.md` — Skill dependency graph and data flow.
- `references/situations.md` — Expanded situation handlers (15+).
- `references/frameworks.md` — Decision frameworks (10).
- `references/resources.md` — Professional referral resources.

## Rules

- One question at a time. Never batch.
- Anti-platitude rules are non-negotiable. Read ETHOS.md.
- Every session ends with one concrete 48-hour assignment.
- Quote the person's words back to them.
- Name contradictions directly.
- If crisis detected, stop workflow and prioritize safety.

## Troubleshooting

If skills aren't found, run:
```
cd ~/.claude/skills/idkwtd && chmod +x setup && ./setup
```
