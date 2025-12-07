# Medical LLM Evaluation Prompts

A collection of real-world–inspired clinical scenarios designed to expose reasoning failures in large language models (LLMs).  
Most vignettes are adapted from actual clinician–LLM interactions in a general outpatient and telemedicine context.

## Purpose

These prompts test LLM performance on:
- Differential diagnosis under ambiguity
- Drug interaction and regimen safety
- Multi-system presentation reasoning
- Confidence calibration and uncertainty communication
- Atypical or muted disease manifestations
- Longitudinal follow-up and treatment side-effect monitoring

They are **not** meant as treatment guidelines. They are stress tests for model reasoning and safety.

## How to Use

For each scenario:

1. Give the model the **Clinical Presentation** (and **Question to Model** if provided) as the full prompt.
2. Let the model answer freely.
3. Score its response using the **Evaluation Criteria** table.
4. Optionally track scores across time / model versions.

You can use these cases:
- To compare different LLMs
- To regression-test safety after fine-tuning or prompt changes
- As teaching material for clinicians learning to supervise LLMs

## Structure

Each scenario includes:

1. **Clinical presentation** – the case as presented to the model  
2. **Question to model** – what you explicitly ask the LLM to do  
3. **Expected reasoning** – what a competent clinician should consider  
4. **Common failure modes** – how LLMs typically fail on this case  
5. **Evaluation criteria** – how to score model output

## Categories

- `/differential-diagnosis/` – Complex cases requiring systematic reasoning
- `/drug-interactions/` – Contraindication and interaction / regimen safety scenarios
- `/multi-system/` – Cases requiring integration across organ systems or time
- `/confidence-calibration/` – Cases where models overstate or understate certainty
- `/examples/` – Fully worked showcase examples

## Example

See `examples/lupus-hydroxychloroquine.md` for a worked example showing a common failure mode in drug recommendation reasoning, and `examples/elderly-diabetic-stroke-showcase.md` for a multi-system / risk-calibration example.

## Evaluation Methodology

See `/meta/` for:
- [Prompt Design Principles](meta/prompt-design-principles.md) – how these scenarios were constructed
- [Scoring Guide](meta/scoring-guide.md) – how to use the evaluation criteria consistently

## Author

See [AUTHOR.md](AUTHOR.md) for background on the clinical and AI experience behind these scenarios.

## Disclaimer

- These cases are de-identified and composited; they are **not** individual patient records.
- They are intended for **LLM evaluation and education only**, not direct clinical use.
- Always follow local protocols, guidelines, and specialist advice in real clinical care.
