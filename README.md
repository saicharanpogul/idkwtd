# IDKWTD — I Don't Know What To Do

A structured life direction skill stack for Claude Code. 9 interconnected
skills that help people who feel stuck find their next move.

Not therapy. Not career coaching. Not motivational posters. A rigorous
thinking partner that asks hard questions, names what it sees, and
produces concrete action plans.

---

## Why This Exists

More people have more options than at any point in history. And more
people feel more stuck than at any point in history. The problem is not
information or motivation. The problem is the absence of structured
thinking applied to life decisions.

Every AI career tool starts with "what job do you want?" IDKWTD starts
with "what's actually happening to you right now?" Because most stuck
people don't need a job recommendation. They need someone to help them
see their situation clearly.

---

## The Stack

| Skill | Time | Purpose |
|-------|------|---------|
| `/session` | 40-60min | Full diagnostic. Entry point. Produces a Direction Document. |
| `/check-in` | 15min | Follow up on assignments. Accountability. |
| `/reality-check` | 5min | Quick gut check on a specific decision. |
| `/fear-audit` | 20min | Deep dive into what's blocking action. |
| `/options-lab` | 20min | Brainstorm and stress-test options. |
| `/momentum` | 10min | Cross-session pattern analysis. |
| `/money-map` | 15min | Financial clarity and runway. |
| `/skill-scan` | 15min | Evidence-based skills inventory. |
| `/network-map` | 15min | Map relationships and opportunities. |

Skills are interconnected. `/session` generates a Direction Document that
`/check-in` reads. `/momentum` reads ALL sessions and finds patterns.
`/fear-audit` deep-dives into blockers identified in `/session`. The
value compounds with each session. See `ARCHITECTURE.md` for the full
dependency graph.

---

## How It Works

### `/session` detects six modes of stuck

| Mode | You said... | The approach |
|------|------------|--------------|
| Recovery | "I just lost my job" | Stabilize, then direction |
| Escape | "I'm trapped" | Map costs of leaving vs staying |
| Filter | "Too many options" | Build decision criteria |
| Discovery | "No idea what to do" | Surface hidden strengths |
| Decision | "I'm at a crossroads" | Structured decision framework |
| Excavation | "I just feel lost" | Find the root cause |

### `/fear-audit` classifies four types of fear

| Type | What it is | The approach |
|------|-----------|--------------|
| Legitimate | Real risk, real stakes | Plan for it |
| Paper Tiger | Low probability, high drama | Expose the disproportion |
| Identity | Fear of who you'd become | Separate identity from outcome |
| Proxy | The stated fear covers a deeper one | Name the real fear |

### Anti-platitude system

IDKWTD explicitly bans 10 common useless phrases and explains why each
is banned. Instead of "follow your passion," it asks "what's one thing
you did where you lost track of time?" Instead of "believe in yourself,"
it says "here's the evidence that you're actually good at this."

### Session persistence

Every session writes to `~/.idkwtd/sessions/` with YAML frontmatter.
Sessions reference each other. `/momentum` reads all of them to find
patterns you can't see from a single session. Assignments are tracked
with deadlines and `/check-in` holds you accountable.

---

## Installation

### Claude Code

```bash
# Clone to your skills directory
git clone https://github.com/saicharanpogul/idkwtd.git ~/.claude/skills/idkwtd

# Run setup
cd ~/.claude/skills/idkwtd && chmod +x setup && ./setup
```

Then add to your project's `CLAUDE.md`:
```
Skills available:
  /session        — Full life direction diagnostic
  /check-in       — Follow up on a previous session
  /reality-check  — Quick gut check on a decision
  /fear-audit     — Deep dive into what's blocking you
  /options-lab    — Brainstorm and stress-test options
  /momentum       — Track progress across sessions
  /money-map      — Financial clarity and runway
  /skill-scan     — Evidence-based skills inventory
  /network-map    — Map your people and opportunities
```

### Claude Projects (alternative)

Copy `session/SKILL.md` into a Claude Project system prompt for the core
experience. For the full stack, copy the skill you need. Each skill
works standalone but gains power from the interconnections.

### Just Reading It

The `ETHOS.md` and `references/frameworks.md` files contain thinking
tools that work even without Claude. Read them.

---

## Recommended Flows

**First time, deeply stuck:**
`/session` → wait 7 days → `/check-in`

**Specific decision right now:**
`/reality-check` (standalone, 5 minutes)

**Don't know what I'm good at:**
`/skill-scan` → `/session`

**Scared to act on my direction:**
`/fear-audit` → `/options-lab`

**Money is the blocker:**
`/money-map` → `/session` (with financial constraints clarified)

**Been at this for a while:**
`/momentum` (after 3+ sessions)

**Need to find opportunities:**
`/skill-scan` → `/network-map`

---

## Project Structure

```
idkwtd/
├── setup                    # One-command installer
├── ETHOS.md                 # Philosophy: 8 principles
├── ARCHITECTURE.md          # Skill dependency graph
├── CONTRIBUTING.md          # How to contribute
├── CHANGELOG.md             # Version history
├── bin/                     # Infrastructure
│   ├── idkwtd               # Unified CLI dispatcher
│   ├── idkwtd-config        # Config management
│   ├── idkwtd-sessions      # Session listing
│   ├── idkwtd-analytics     # Usage dashboard
│   ├── idkwtd-progress      # Progress tracker
│   └── idkwtd-uninstall     # Clean removal
├── session/SKILL.md         # Full diagnostic (688 lines)
├── check-in/SKILL.md        # Accountability follow-up
├── reality-check/SKILL.md   # Quick decision check
├── fear-audit/SKILL.md      # Fear decomposition
├── options-lab/SKILL.md     # Options brainstorming
├── momentum/SKILL.md        # Pattern analysis
├── money-map/SKILL.md       # Financial clarity
├── skill-scan/SKILL.md      # Skills inventory
├── network-map/SKILL.md     # Relationship mapping
└── references/              # Deep reference material
    ├── situations.md        # 15+ situation handlers
    ├── frameworks.md        # 10 decision frameworks
    └── resources.md         # Professional referrals
```

---

## What Makes This Different

**vs. AI career tools** (Apt, CareerVillage Coach, Google Career Dreamer):
Those answer "what job should I get." IDKWTD answers "I don't know what's
wrong and I can't think clearly." Different starting point, different tool.

**vs. therapy apps** (BetterHelp, Flourish, Purpose):
Those are mental health tools. IDKWTD is a thinking tool. If you need
therapy, get therapy. If you need structured thinking about your next move,
use this.

**vs. a single ChatGPT prompt:**
Anyone can ask ChatGPT "I'm stuck, help me." The difference is 9
interconnected skills with session persistence, accountability tracking,
cross-session pattern analysis, anti-platitude enforcement, evidence-based
methods, and a reference library of situation handlers and decision
frameworks. The system is the moat, not any single prompt.

---

## Design Influences

- **gStack** by Garry Tan — Structural inspiration. Phased workflows,
  anti-sycophancy rules, skill interconnection, document output.
- **YC Office Hours** — The questioning philosophy. Earn the right to
  advise by understanding first.
- **Motivational Interviewing** — Therapeutic technique adapted for
  non-clinical use. Reflect, don't prescribe.
- **Behavioral Economics** — Constraint-based decision making, loss
  aversion awareness, reversibility testing.

---

## Contributing

See `CONTRIBUTING.md`. The highest-value contribution is adding situation
handlers to `references/situations.md`. If you've been through something
and you know what helps, write it down.

---

## License

MIT. Do whatever you want with it. If it helps one person get unstuck,
it was worth building.

---

Built by [@pogul_saicharan](https://x.com/pogul_saicharan) during a weekend
break from [Roaster V2](https://roaster.fun).

Because sometimes the builder needs building too.
