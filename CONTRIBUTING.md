# Contributing to Epistemic Honesty

Thanks for wanting to improve this skill.

---

## What to contribute

**Good contributions:**
- New worked examples in `EXAMPLES.md` (especially failure modes caught in production)
- New decay rules discovered through real use
- Clarifications to existing principles where ambiguous
- Model-specific behavior notes (how a specific model interprets the rules)
- Compatibility guides for new agent platforms

**Out of scope:**
- Changing the four core principles fundamentally — this is a stable behavioral contract
- Adding a fifth principle — keep it four, keep it memorable
- Model-specific forks — the skill should work for any model

---

## How to contribute

1. Fork the repo
2. Make your change in a branch
3. Test it: run the skill on at least 3 real prompts and verify the output matches the principles
4. Open a PR with a concrete description of what changed and why
5. Include before/after examples in the PR description

---

## Reporting a failure mode

If the skill failed — the AI asserted a fabricated fact, the confidence was wrong,
the boundary statement was skipped — please open an issue with:

- The exact prompt
- The AI response (what it said)
- What it should have said (which principle was violated)
- Which model you were using

These become the next version's worked examples and decay rules.

---

## Versioning

This skill uses semantic versioning.

- **Patch (1.0.x):** Clarifications, example additions, typo fixes. No behavior change.
- **Minor (1.x.0):** New decay rules, new model notes, new examples. Backward compatible.
- **Major (x.0.0):** Changes to the four principles or the confidence math. Rare.

---

*Small improvements compound. Every real failure mode added to EXAMPLES.md is one fewer invisible hallucination for the next user.*
