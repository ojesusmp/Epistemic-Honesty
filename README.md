# Epistemic Honesty

> Stop your AI from sounding certain when it's guessing.

A four-principle discipline that forces any AI agent — Claude, GPT, Gemini, or any other model — to tell you where its information came from and how confident it actually is.

---

## The Problem It Solves

When you ask an AI a question, it answers in the same confident tone whether it is:
- Reading from a verified document you gave it
- Recalling something from months-old training data
- Guessing based on a vague pattern
- Inventing a detail with no basis at all

You cannot tell which one is happening. This skill makes it visible.

---

## What It Does

Every factual claim gets tagged with its source type and a confidence percentage:

```
Your meeting with the client is on Thursday, March 15 [VAULT: 94%].
The average churn rate for SaaS is around 5–7% [KNOWN: 60%].
⚠️ I don't have the contract amount in your records. [INFERRED: 35%]. Verify before acting.
```

Now you can see:
- `VAULT: 94%` → pulled from your actual records, high confidence
- `KNOWN: 60%` → from AI training data, moderate confidence
- `INFERRED: 35%` + ⚠️ → AI is reasoning without a source, low confidence

---

## The Four Principles

### 1. TRACE — Know the source before claiming

Before asserting any fact, the AI classifies where it came from:

| Label | Meaning | Confidence |
|-------|---------|-----------|
| `VAULT` | From your memory, vault, emails, or documents | 90–99% |
| `DERIVED` | Calculated from verified sources | 80–95% |
| `KNOWN` | From AI training data | 40–75% |
| `INFERRED` | Reasoned with no direct source | 20–50% |
| `FABRICATED` | No traceable source — **never asserted** | Never |

If classification lands on `FABRICATED`, the AI stops and tells you the gap instead of inventing an answer.

### 2. SCORE — Attach a confidence percentage

Every non-trivial claim gets a number. The number goes down (decays) when:
- The source record is older than 90 days (−15%)
- The AI is chaining multiple uncertain steps (−10% per step)
- The claim involves events after the AI's training cutoff (−30%)

No rounding up. A 72% is reported as 72%, not 80%.

### 3. VERIFY — Act on low confidence before answering

The score triggers an action:

| Score | What the AI does |
|-------|----------------|
| 90–100% | Answers directly with tag |
| 80–89% | Answers with tag + notes why it is not 100% |
| 60–79% | Checks your records first; if not found, says so explicitly |
| 50–59% | Prefixes "I'm not certain —" and names what would confirm it |
| Below 50% | Prefixes ⚠️ and tells you to verify independently |

The AI checks **before** answering, not after. No "here is your answer, oh by the way I'm not sure."

### 4. FLAG — Name the hallucination boundary

When the AI is generating specific details with no source — a meeting date, a contract term, a person's role — it must stop and say:

```
I don't have [specific thing] in your records.
Answering from [KNOWN/INFERRED] at [XX%].
You should verify this before acting on it.
```

It cannot soften this into "I believe" or "I think." Those phrases hide the problem. One invented detail in a response flags the whole response.

---

## Install

### Claude Code

```bash
git clone https://github.com/ojesusmp/Epistemic-Honesty ~/.claude/skills/epistemic-honesty
```

Then invoke in Claude Code:
```
/epistemic-honesty
```
Or use any alias: `/epistemic`, `/truthcheck`, `/confidence`, `/honesty`, `/verify-facts`

### Hermes Agent

```bash
mkdir -p ~/.hermes/profiles/<your-profile>/skills/epistemic-honesty
cp epistemic-honesty/SKILL.md ~/.hermes/profiles/<your-profile>/skills/epistemic-honesty/
```

Restart your Hermes gateway. The skill auto-loads.

### OpenAI / Custom Agents

Copy the contents of `SKILL.md` into your system prompt or agent instructions. The principles are model-agnostic — they work as behavioral instructions for any model.

---

## Quick Start

Once installed, you can invoke it directly:

**Claude Code:**
```
/epistemic-honesty
What was the decision we made about the API design last month?
```

**Inline in a prompt:**
```
Apply epistemic honesty principles.
What is the renewal date for the Acme contract?
```

**The AI will:**
1. Check its memory/vault first
2. If found: answer with `[VAULT: XX%]`
3. If not found: say "Not in current records — [KNOWN/INFERRED: XX%]"
4. Never invent a date and present it as a fact

---

## Model Compatibility

| Model | Level | What you get |
|-------|-------|-------------|
| Claude Opus | Full | All 4 principles, full scoring, decay math, boundary flags |
| Claude Sonnet | Full | All 4 principles, full scoring |
| Claude Haiku | Lite | Source labels only (no % scores), boundary flags required |
| GPT-4o | Full | All 4 principles (paste SKILL.md into system prompt) |
| Gemini | Full | All 4 principles (paste SKILL.md into system prompt) |
| Any model | Lite | Add `--haiku` flag to use label-only mode |

---

## When to Use It

**Good fits:**
- Asking about records, contracts, past decisions, client details
- Any question where you need to know if the AI is guessing
- High-stakes answers (dates, money, health, legal)
- Agents with memory systems (Hindsight, vault, RAG)

**Not needed for:**
- Brainstorming ("give me 5 ideas for...")
- Creative tasks with no factual claims
- Simple direct-answer questions from a document in context

---

## Files

| File | Purpose |
|------|---------|
| `SKILL.md` | Canonical skill definition — all four principles in full |
| `README.md` | This file — plain-language guide |
| `EXAMPLES.md` | Worked examples with real input/output pairs |
| `CHANGELOG.md` | Version history |
| `CONTRIBUTING.md` | How to improve this skill |
| `SECURITY.md` | Security and responsible use |

---

## License

MIT — see [LICENSE](./LICENSE).

*Designed by Orlando Molina / TruePointAgents*
