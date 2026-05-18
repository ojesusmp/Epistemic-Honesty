# Changelog

All notable changes to Epistemic Honesty are documented here.

Format follows [Keep a Changelog](https://keepachangelog.com/en/1.0.0/).
Versioning follows [Semantic Versioning](https://semver.org/).

---

## [1.1.0] - 2026-05-18

### Added
- **CONTEXT source tier** — content present in the current session (system prompt, injected documents, user messages, `FACTS` blocks). Baseline confidence 92–99%. Closes the 90%+ gap for vault-free sessions.
- **Citation requirement** — every CONTEXT claim must carry a verbatim quote of its source span: `[claim] [CONTEXT: XX% | "quote"]`. No quote → claim downgrades to INFERRED or FABRICATED.
- **Pre-response audit pass** — per-claim silent check that routes each factual claim to its correct source tier before output.
- **FACT INJECTION PROTOCOL** — structured `FACTS` block users can paste at session start; each line becomes a CONTEXT-tier fact at 95% baseline. Vault replacement for sessions with no external memory.
- **CONTEXT decay rules** — three penalties (paraphrased quote −10%, user statement vs document −5%, transcript vs primary −10%).
- EXAMPLES 11–13: CONTEXT tier from injected doc, FACTS block injection, fabricated CONTEXT quote caught.

### Changed
- Source tier table (SKILL.md, README.md) now leads with CONTEXT as the most-verifiable tier.
- Haiku / lite mode: CONTEXT quote requirement holds at all tiers — the verbatim quote is the proof, not the percentage.
- DERIVED definition now accepts CONTEXT as a verified input source.

### Design notes
- The quote requirement makes fabricated citations **detectable, not impossible** — the user can spot-check any CONTEXT quote against the conversation. A quote that does not appear in context reclassifies the whole claim as FABRICATED. Honest framing documented in SECURITY.md.
- Zero new external dependencies — CONTEXT uses the context window itself as the verifiable substrate. Backward compatible with VAULT.

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
