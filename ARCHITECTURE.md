# IDKWTD Architecture

## Skill Dependency Graph

```
                    ┌─────────────┐
                    │  /session   │  ← Entry point. Full diagnostic.
                    │  (40-60min) │    Produces Direction Document.
                    └──────┬──────┘
                           │
              ┌────────────┼────────────┐
              │            │            │
              ▼            ▼            ▼
      ┌──────────┐  ┌───────────┐  ┌──────────┐
      │/check-in │  │/fear-audit│  │/options-  │
      │ (15min)  │  │ (20min)   │  │   lab     │
      │          │  │           │  │ (20min)   │
      └────┬─────┘  └───────────┘  └──────────┘
           │
           ▼
      ┌──────────┐
      │/momentum │  ← Reads ALL sessions. Pattern recognition.
      │ (10min)  │
      └──────────┘

  ┌──────────┐  ┌──────────┐  ┌──────────┐
  │/reality- │  │/money-   │  │/skill-   │
  │  check   │  │  map     │  │  scan    │
  │ (5min)   │  │ (15min)  │  │ (15min)  │
  └──────────┘  └──────────┘  └──────────┘
                                    │
                               ┌────┘
                               ▼
                          ┌──────────┐
                          │/network- │
                          │  map     │
                          │ (15min)  │
                          └──────────┘
```

## Data Flow

All sessions write to `~/.idkwtd/sessions/`. The filename convention is:
`{skill}-{username}-{YYYYMMDD-HHMMSS}.md`

This means:
- /check-in can find previous /session documents
- /momentum can scan ALL documents chronologically
- /fear-audit can reference constraints from a prior /session
- /network-map can reference strengths from /skill-scan

## Skill Descriptions

| Skill | Purpose | Input | Output |
|-------|---------|-------|--------|
| /session | Full diagnostic. Entry point. | Person's situation | Direction Document |
| /check-in | Accountability follow-up | Previous Direction Document | Progress Report |
| /reality-check | Quick gut check on one decision | A specific decision | Go/No-Go Assessment |
| /fear-audit | Deep dive into blockers | A fear or blocker | Fear Decomposition Document |
| /options-lab | Brainstorm and stress-test | A problem space | Options Matrix |
| /momentum | Cross-session pattern analysis | All prior sessions | Momentum Report |
| /money-map | Financial clarity | Income/expenses/runway | Financial Reality Document |
| /skill-scan | Evidence-based skills inventory | Work history/behaviors | Skills Portfolio |
| /network-map | Relationship and opportunity map | People they know | Network Action Plan |

## Recommended Flows

**First time, deeply stuck:** `/session` → wait 7 days → `/check-in`

**Specific decision looming:** `/reality-check` (standalone, 5 minutes)

**Stuck on finances:** `/money-map` → `/session` (with financial constraints clarified)

**Don't know what I'm good at:** `/skill-scan` → `/session` or `/options-lab`

**Tried something, need to recalibrate:** `/check-in` → `/momentum` (after 3+ sessions)

**Scared to act:** `/fear-audit` → `/options-lab` → `/session`

**Need to leverage relationships:** `/skill-scan` → `/network-map`

## Session Persistence

Sessions are Markdown files in `~/.idkwtd/sessions/`. They follow a
consistent header format so skills can parse them:

```markdown
---
skill: session
date: 2026-03-28T14:30:00Z
mode: escape
status: active
assignment: "message three people in fintech"
assignment_deadline: 2026-03-30
tags: [career, stuck, fintech, escape-mode]
---

# Direction Document
...
```

The YAML frontmatter enables:
- Programmatic discovery by other skills
- Filtering by date, mode, status, skill
- Assignment tracking and deadline monitoring
- Tag-based cross-session pattern matching

## Analytics

Usage analytics write to `~/.idkwtd/analytics/`:
- `skill-usage.jsonl` — which skills are used, when, how long
- `assignments.jsonl` — assignments given and their outcomes
- `progress.jsonl` — self-reported progress over time
- `patterns.jsonl` — patterns detected by /momentum

All analytics are local. Nothing is sent anywhere unless the user
explicitly opts into telemetry (off by default).

## Directory Structure

```
idkwtd/
├── setup                    # One-command installer
├── ETHOS.md                 # Philosophical foundation
├── ARCHITECTURE.md          # This file
├── README.md                # Project overview
├── LICENSE                  # MIT
├── CONTRIBUTING.md          # How to contribute
├── CHANGELOG.md             # Version history
├── bin/                     # Infrastructure scripts
│   ├── idkwtd-config        # Config get/set
│   ├── idkwtd-sessions      # Session listing/reading
│   ├── idkwtd-analytics     # Usage dashboard
│   └── idkwtd-progress      # Progress tracker
├── session/SKILL.md         # Full diagnostic
├── check-in/SKILL.md        # Accountability follow-up
├── reality-check/SKILL.md   # Quick decision gut-check
├── fear-audit/SKILL.md      # Fear decomposition
├── options-lab/SKILL.md     # Options brainstorming
├── momentum/SKILL.md        # Cross-session patterns
├── money-map/SKILL.md       # Financial clarity
├── skill-scan/SKILL.md      # Skills inventory
├── network-map/SKILL.md     # Relationship mapping
└── references/              # Deep reference material
    ├── frameworks.md        # Decision frameworks
    ├── situations.md        # Expanded situation handling
    └── resources.md         # Professional resources
```
