# Changelog

All notable changes to Epistemic Honesty are documented here.

Format follows [Keep a Changelog](https://keepachangelog.com/en/1.0.0/).
Versioning follows [Semantic Versioning](https://semver.org/).

---

## [1.0.0] - 2026-05-17

### Added
- **Principle 1: TRACE** — five source type classifications (VAULT, DERIVED, KNOWN, INFERRED, FABRICATED) with baseline confidence ranges
- **Principle 2: SCORE** — inline confidence percentage format `[TYPE: XX%]` with seven decay rules
- **Principle 3: VERIFY** — five confidence threshold bands with required actions per band
- **Principle 4: FLAG** — hallucination boundary statement, silence-is-not-confirmation rule, one-fabrication-voids-response rule
- Source classification quick reference template
- Model compatibility table (Opus/Sonnet full, Haiku lite)
- `--haiku` flag for label-only mode without percentage scores
- Hermes Agent compatibility (SKILL.md frontmatter)
- Claude Code compatibility (argument-hint, model frontmatter fields)

### Design notes
- Karpathy Discipline is the structural model: four principles, one check per principle, explicit failure modes
- Intended as domain-agnostic companion to Karpathy Discipline (which is coding-specific)
- Decay math is deterministic, not LLM-estimated — the agent computes from explicit rules
- FABRICATED is a hard stop, not a label — it triggers the boundary statement, not a tagged claim

---

*Initial release. Designed by Orlando Molina / TruePointAgents.*
