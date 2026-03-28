# Changelog

All notable changes to IDKWTD will be documented in this file.

## [1.0.1] - 2026-03-28

### Improved
- Fixed placeholder URLs in README and session skill
- Added `bin/idkwtd` unified CLI dispatcher
- Added `bin/idkwtd-uninstall` for clean removal
- Added username detection to setup and config
- Expanded international crisis resources (US 988, UK Samaritans, Australia Lifeline, Canada 988, Befrienders Worldwide)
- Fixed `sed -i` macOS compatibility in idkwtd-config
- Cleaned up defensive language in CONTRIBUTING.md

## [1.0.0] - 2026-03-28

### Added
- Initial release with 9 interconnected skills
- `/session` — Full life direction diagnostic (6 modes)
- `/check-in` — Accountability follow-up with assignment tracking
- `/reality-check` — Quick 5-minute decision gut check
- `/fear-audit` — Fear decomposition and classification
- `/options-lab` — Structured brainstorming with stress testing
- `/momentum` — Cross-session pattern analysis and scoring
- `/money-map` — Financial clarity and runway calculation
- `/skill-scan` — Evidence-based skills inventory
- `/network-map` — Relationship and opportunity mapping
- Session persistence in `~/.idkwtd/sessions/` with YAML frontmatter
- Cross-skill routing (skills reference and build on each other)
- Local analytics in `~/.idkwtd/analytics/`
- Infrastructure scripts: `idkwtd-config`, `idkwtd-sessions`,
  `idkwtd-analytics`, `idkwtd-progress`
- Reference docs: `situations.md`, `frameworks.md`, `resources.md`
- `ETHOS.md` — Philosophical foundation
- `ARCHITECTURE.md` — Skill dependency graph and data flow
- `CONTRIBUTING.md` — Contribution guide with style rules
- Anti-platitude system (10 banned phrases with rationale)
- 6 situation modes: Recovery, Escape, Filter, Discovery, Decision, Excavation
- 4 fear classifications: Legitimate, Paper Tiger, Identity, Proxy
- One-command `setup` script
