# Prompt Design Principles for Clinical LLM Evaluation

This repository is **not** about making models look good.  
It is designed to **stress-test failure modes** that matter at the bedside, especially in:

- Resource-limited outpatient settings
- Elderly and multi-morbid populations
- Real-world diagnostic ambiguity and follow-up constraints

This document explains how to design prompts that **expose** those weaknesses rather than hide them.

---

## 1. Start From Real Clinical Workflows

The prompts here are distilled from real clinician–LLM conversations in:

- General outpatient care
- Telemedicine follow-up
- Chronic disease management (HTN, DM, stroke, cancer, etc.)

**Principle:** Begin with how a patient would actually present, not a textbook-perfect case.

- Use realistic partial information.
- Include common confounders (polypharmacy, comorbidities, resource limits).
- Avoid “toy” vignettes with obvious single answers.

---

## 2. Limit Early Information on Purpose

Many LLMs perform well when all labs and imaging are handed to them upfront.

To surface failure modes, prompts here often:

- Provide **only** history and basic exam initially.
- Omit definitive tests (e.g. CT, MRI, advanced serology) at first.
- Use phrases like “assume renal function is normal” only when necessary, to test whether the model actually uses that constraint.

**Goal:** Force the model to reason from incomplete data, like a real clinician at first presentation.

---

## 3. Encode Ambiguity, Not Trick Questions

These scenarios are **not riddles**. They mimic genuine uncertainty:

- Multiple plausible differentials are intentionally left open.
- Presentation is “messy” (e.g. elderly diabetics with fatigue and anaemia).
- Resource availability is varied (e.g. Nigerian outpatient clinic vs tertiary cancer centre).

A good model should:

- Explicitly acknowledge uncertainty.
- Prioritise safety.
- Propose **what to do next**, not just a label.

---

## 4. Bake In Safety-Critical Dependencies

Many failures in LLM output are **missing conditional checks**, for example:

- Recommending ACE inhibitor + Spironolactone without potassium monitoring.
- Suggesting HCQ or MTX without discussing ophthalmologic exam or liver function.
- Treating sepsis as unlikely “because there is no fever” in an elderly diabetic.

Prompts are designed to include **subtle but crucial details**:

- “Elderly, diabetic, no fever” → tests blunted febrile response reasoning.
- “ACEi + Spironolactone + Indapamide” → tests recognition of hyperkalaemia risk.
- “Peau d’orange + 7-month lump” → tests staging and MDT thinking before surgery.

If the model ignores those details, it should be penalised in the evaluation.

---

## 5. Make the Model Expose Its Own Confidence

Several cases in `/confidence-calibration/` explicitly ask the model to:

- Provide a **numerical** or graded confidence score (0–10).
- Explain **why** it is that confident.
- State what would **change its mind** (what new data would matter).

This reveals:

- Overconfidence in weakly supported conclusions.
- False reassurance in high-risk contexts.
- Unwillingness to admit uncertainty or to propose further workup.

**Design pattern:**

> “How likely is X versus Y? Give a 0–10 confidence rating and explain your reasoning, including what you would do next.”

---

## 6. Force Interaction With Resource and Context Constraints

Real-world practice is constrained by:

- Limited imaging
- Cost barriers
- Local antibiotic resistance patterns
- Access to oncology services

Prompts therefore:

- Specify “resource-limited outpatient clinic” or “basic oncology services available but delayed”.
- Look for whether the model continues to recommend unrealistic, high-resource investigations and drugs **only**, or whether it proposes staged, context-aware alternatives.

This helps distinguish **guideline-dumping** from **contextual reasoning**.

---

## 7. Ask for Process, Not Just Outcome

The evaluation criteria reward **how** the model thinks, not just whether it names the “right” diagnosis.

Prompts often ask explicitly for:

- Working diagnosis **plus** differentials.
- Next best step, not full long-term management.
- Safety-netting and follow-up plans.

A model that guesses the correct diagnosis but:

- Ignores differentials,
- Fails to mention red flags,
- Or omits simple safety-net advice

should still lose points.

---

## 8. Keep Prompts Stable for Comparability

For benchmarking across models:

- Do **not** modify the core clinical presentation or question once you start comparing models.
- If you change a scenario, version it (e.g. `v1`, `v2`) and note the differences.
- Use the same prompt wording when re-testing after fine-tuning or system changes.

This ensures that differences in scores reflect **model changes**, not prompt drift.

---

## 9. Document the Trap Explicitly in the Scenario File

Each `.md` scenario includes a **“Common LLM Failure Modes”** section.

When designing new prompts:

1. Start by asking: *“What subtle but important thing do I expect a weak model to miss here?”*
2. Encode that subtlety in the case (e.g. comorbidity, drug combination, atypical presentation).
3. Write those expected failures down explicitly, so scorers know what to look for.

This keeps the repo honest: **we are not ambushing the model — we are intentionally testing known weak spots.**

---

## 10. Align Prompt Design With Clinical Ethics

These prompts are built with a simple ethic:

> *If a junior colleague gave this answer in clinic, would I be worried?*

Prompts are therefore designed so that:

- Safe, humble, guideline-aware reasoning scores highly.
- Overconfident, unsafe advice scores poorly even if it “sounds smart.”

When you design new cases, keep that ethical lens front-and-centre.
