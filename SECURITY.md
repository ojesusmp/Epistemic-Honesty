# Security and Responsible Use

---

## What this skill does and does not do

**Does:**
- Instruct AI agents to label their confidence and source type
- Prevent confident-sounding hallucinations by requiring explicit uncertainty disclosure
- Improve human decision-making by making AI uncertainty visible

**Does not:**
- Prevent an AI model from hallucinating at the model level
- Guarantee that `[VAULT: 94%]` claims are actually correct
- Replace human verification for consequential decisions

---

## Responsible use

This skill reduces hallucination risk — it does not eliminate it. The confidence
percentages are the AI's self-assessment, not ground truth.

**Always verify independently for:**
- Legal decisions, contracts, deadlines
- Medical or health-related claims
- Financial figures, budgets, account numbers
- Any claim where being wrong has real cost

A response tagged `[VAULT: 91%]` means the AI retrieved it from a record and
assessed 91% confidence. It does not mean the record was accurate, complete,
or current. Your records can be wrong too.

---

## The CONTEXT tier and fabricated quotes

The `CONTEXT` tier (added in v1.1) requires every claim to carry a verbatim quote
from the session. This is an **honesty mechanism, not a technical guardrail.**

What it does:
- Makes a fabricated CONTEXT claim **detectable** — the user can scan the
  conversation and confirm the quote is real.

What it does NOT do:
- It cannot **prevent** an AI from generating a fake quote. A model can still
  produce `[CONTEXT: 96% | "..."]` with a quote that never appeared in context.

The defense is the user. For consequential facts (money, dates, legal, health),
**spot-check CONTEXT quotes** against the actual conversation. A quote you cannot
find means the claim is fabricated — treat it as `FABRICATED`, not `CONTEXT`.

The quote requirement shifts fabrication from invisible to checkable. It does not
remove the need for human verification.

---

## Reporting issues

If you find a prompt that causes the skill to fail silently — asserting a fabricated
fact without flagging it — please open an issue at:

https://github.com/ojesusmp/Epistemic-Honesty/issues

Include the prompt, the response, and the model used. These become the next
version's test cases.

---

*The skill is a behavioral contract, not a technical guardrail.*
*Human judgment is still the final check.*
