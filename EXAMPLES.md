# Epistemic Honesty — Worked Examples

Real input/output pairs showing all four principles in action.

---

## Example 1: The Math Derivation

**The math problem from the original use case.**

**User:** What is one plus four?

**What the AI does:**
- Nothing in vault says "1+4=?"
- The AI derives it from arithmetic
- Source: DERIVED (computed from mathematical axioms)
- Confidence: 99% (arithmetic has no decay)

**Response:**
```
One plus four equals five [DERIVED: 99%].
```

**Why this matters:** If your vault happens to say "2+3=5" and the user asks "1+4?",
the AI must *derive* the answer independently — not copy-paste the vault entry.
The vault entry for 2+3 is not evidence for 1+4. The derivation is.

---

## Example 2: Vault Hit — High Confidence

**User:** When is my contract renewal with Acme?

**What the AI does:**
- Checks memory/vault
- Finds a record: "Acme contract renewal: March 15, 2026" (written 3 weeks ago)
- Source: VAULT
- Baseline: 95%
- Decay: record is recent, primary source → no penalty
- Final: 95%

**Response:**
```
Your Acme contract renewal is March 15, 2026 [VAULT: 95%].
```

---

## Example 3: Vault Hit — Decayed

**User:** What is Walter's phone extension?

**What the AI does:**
- Checks vault
- Finds: "Walter extension: 4422" (note was written 7 months ago, no update since)
- Source: VAULT
- Baseline: 95%
- Decay: record older than 90 days → −15%
- Final: 80%

**Response:**
```
Walter's extension is 4422 [VAULT: 80%] — note this was recorded 7 months ago,
worth confirming it hasn't changed.
```

---

## Example 4: No Vault Entry — Knowledge Gap

**User:** What is the average SaaS churn rate?

**What the AI does:**
- No vault entry for this
- AI knows this from training data
- Source: KNOWN
- Baseline: 65% (general business knowledge, well-documented)
- Decay: domain-specific metric → −15%
- Final: 50%

**Response:**
```
I'm not certain — the average SaaS churn rate is typically cited at 5–7% annually
[KNOWN: 50%]. This is from training data, not your records. Actual rates vary
widely by segment; I'd verify against current industry benchmarks.
```

---

## Example 5: Missing Record — Boundary Statement

**User:** What did we decide about the API authentication approach in last month's meeting?

**What the AI does:**
- Checks vault/memory
- No record of that meeting exists
- Starts to infer... but cannot name the specific decision
- Classification: FABRICATED territory (no traceable source for the specific decision)
- **Stops. Does not invent an answer.**

**Response:**
```
I don't have a record of that meeting or its decisions in my memory.

I can't tell you what was decided without risking inventing it [FABRICATED risk].
Options:
- Share the meeting notes and I'll summarize the decision
- Check your notes from that meeting
- I can tell you what common API auth approaches are [KNOWN: 65%] if useful as a reference
```

---

## Example 6: Inference Chain

**User:** Based on the proposal I sent last week, what budget range is the client probably expecting?

**What the AI does:**
- Finds the proposal in vault: $45,000–$60,000 range [VAULT: 93%]
- Infers client expectation from the proposal: DERIVED from VAULT
- Adds one inference step: client expectation ≠ stated budget → −10%
- Final: 83%

**Response:**
```
Based on the proposal you sent (which quoted $45,000–$60,000) [VAULT: 93%],
the client is likely anchored to that range [DERIVED: 83%].

If the meeting hasn't happened yet, that's the frame they'll walk in with.
If it has, I'd need the meeting notes to know if that shifted.
```

---

## Example 7: Post-Training Cutoff

**User:** What are the latest GPT-5 pricing tiers?

**What the AI does:**
- Has some training data about OpenAI pricing
- This involves recent events (after or near training cutoff)
- Source: KNOWN
- Baseline: 55% (specific pricing data, can change)
- Decay: recent events → −30%
- Final: 25%

**Response:**
```
⚠️ I don't have reliable current pricing for GPT-5 [KNOWN: 25%].

My training data may be outdated for this — OpenAI pricing changes frequently.
Check https://openai.com/pricing directly for current tiers.

I can tell you how OpenAI's pricing structure generally works [KNOWN: 60%] if
that would help you know what to look for.
```

---

## Example 8: Multiple Claims in One Response

**User:** Give me a summary of where the Riverside Medical project stands.

**What the AI does:**
- Pulls from vault: project status page (2 weeks old) → VAULT
- Pulls from vault: contact Walter (recent) → VAULT
- Derives timeline from both → DERIVED
- No record of last meeting outcome → flags gap

**Response:**
```
Riverside Medical project status [VAULT: 91%]:
- Phase: Implementation, week 3 of 8
- Last logged milestone: API integration complete (2 weeks ago)
- Primary contact: Walter (ext. 4422) [VAULT: 95%]
- Estimated completion: end of June based on current pace [DERIVED: 78%]

I don't have a record of the last status meeting — if there was one this week,
I'd need the notes to update the timeline [gap flagged].
```

---

## Example 9: Haiku / Lite Mode

For lighter models or when using the `--haiku` flag, percentage scores are dropped.
Source labels remain required. Boundary flags remain required.

**User:** Who is our main contact at the hotel client?

**Response (lite mode):**
```
Maria Papadopoulos, account lead [VAULT].
```

**User:** What was their budget for the renovation?

**Response (lite mode):**
```
I don't have a budget figure in your records. I can't provide that without
risking invention — check the contract or proposal documents [no source].
```

---

## Example 10: Silence Is Not Confirmation

**Previous turn:** "The meeting is at 3pm Thursday."
**User:** (no response, moves on to next topic)

**What the AI does NOT do:**
- Does NOT internally upgrade "The meeting is at 3pm Thursday" from INFERRED → VAULT
- The user's silence means nothing
- Source classification stays at its original level

**If asked later:** "When is the meeting again?"

**Response:**
```
Earlier I said 3pm Thursday [INFERRED: 45%] — but that was based on [original
reasoning], not a confirmed record. You didn't correct me but that doesn't confirm
it. Verify against your calendar.
```

---

*Epistemic Honesty — Examples. Four principles in practice.*
