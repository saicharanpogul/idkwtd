# Contributing to IDKWTD

IDKWTD is open source and contributions are welcome. This document explains
how the project is structured so you can contribute effectively.

---

## Philosophy

The goal is to make IDKWTD so comprehensive that someone who wants to
improve it contributes HERE rather than building a competing skill from
scratch. The bar for contribution is: "Does this make the tool better for
someone who's stuck?"

---

## What to Contribute

### High-value contributions

1. **New situation handlers in `references/situations.md`**
   The most impactful contribution. If you've been through a specific
   life situation and know what helps/doesn't help, add a section.
   Follow the existing format: emotional state, common mistakes,
   IDKWTD approach.

2. **New decision frameworks in `references/frameworks.md`**
   If you know a decision framework that helps stuck people, add it.
   Include: what it is, why it works, which skills use it.

3. **Improvements to existing skills**
   If a skill asked a question that didn't help, or missed a question
   that would have helped, improve it. The skills are the core product.

4. **Localization and cultural context**
   IDKWTD was written from one cultural perspective. Different cultures
   have different relationships with family expectations, career paths,
   financial norms, and life transitions. Adding cultural context to
   `references/situations.md` is extremely valuable.

5. **Professional resources in `references/resources.md`**
   Country-specific mental health resources, career services, financial
   aid programs. These save lives.

### Medium-value contributions

6. **New skills** (if genuinely different from existing ones)
   Before proposing a new skill, check if the functionality could be
   added to an existing skill. The skill count should grow slowly.
   A new skill needs: clear trigger phrases, unique value vs existing
   skills, integration with session persistence, routing to/from other
   skills.

7. **Bin scripts and infrastructure**
   Better analytics, session management, progress tracking.

8. **Testing and evaluation**
   Run IDKWTD sessions (even simulated ones) and report what worked
   and what didn't. This feedback is gold.

### Lower-value contributions

9. **README improvements** — always welcome but not the core product
10. **Typo fixes** — appreciated, especially in skill prompts where
    clarity matters

---

## How to Contribute

### For situation handlers and frameworks

1. Fork the repo
2. Edit `references/situations.md` or `references/frameworks.md`
3. Follow the existing format
4. Submit a PR with a brief description of why this situation/framework
   matters

### For skill improvements

1. Fork the repo
2. Edit the relevant `SKILL.md`
3. Test by running the skill yourself (see Testing below)
4. Submit a PR with: what you changed, why, and how it went when you tested

### For new skills

1. Open an issue first describing the proposed skill
2. Wait for discussion — someone may suggest it fits in an existing skill
3. If approved, create the skill directory with SKILL.md
4. Include: YAML frontmatter, preamble, phases, output format, routing
5. Submit PR

---

## Testing

The best test is running the skill yourself. Use Claude Code or paste the
SKILL.md into a Claude Project system prompt.

### What to test

- Does the opening question feel right? Does it cover the person's situation?
- Do the follow-up questions go deep enough?
- Does the output (Direction Document, etc.) feel useful and specific?
- Does the routing to other skills make sense?
- Are the anti-platitude rules working? (No generic motivational language)

### How to report

In your PR, include:
- Which skill you tested
- Your simulated scenario (what situation you described)
- What worked well
- What felt generic, unhelpful, or wrong
- Suggested changes

---

## Style Guide

### Language
- Write like you're talking to a friend. Not a textbook.
- Be direct. "Do this" not "you might want to consider doing this."
- No jargon unless the person introduced it first.
- No emojis in skill files.

### Structure
- One question per AskUserQuestion call. Always.
- Every phase has a clear input, process, and output.
- Every skill routes to at least one other skill.
- Every skill writes to `~/.idkwtd/sessions/`.

### Anti-patterns (don't do these)
- Don't add motivational quotes
- Don't add "affirmations" or "positive thinking" exercises
- Don't add personality quizzes or Myers-Briggs style assessments
- Don't add gamification (points, badges, streaks)
- Don't add social features (sharing, comparing, leaderboards)
- Don't make it longer just to make it longer

---

## Code of Conduct

Be kind. Be specific. Be useful. Remember that the people using this
tool are genuinely struggling, and every word in these skills will be
read by someone who's having a hard time.

---

## License

All contributions are under MIT license. By submitting a PR, you agree
to license your contribution under MIT.
