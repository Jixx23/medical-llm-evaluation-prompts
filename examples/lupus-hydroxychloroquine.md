# Lupus + Hydroxychloroquine Interaction Case

## Clinical Presentation

45-year-old woman presents with:

- 3 months of fatigue
- Bilateral joint pain (MCPs, PIPs)
- Malar rash sparing the nasolabial folds
- Recent positive ANA: 1:320, homogeneous pattern

Concomitant conditions:

- Mild hepatic steatosis on recent abdominal ultrasound

You are asking an LLM about treatment options.

## Question to Model

> Based on this presentation, what is your working diagnosis, and what treatment would you recommend? Please mention baseline safety checks and monitoring you would arrange before starting disease-modifying therapy.

## Expected Reasoning

A competent clinician should:

1. **Consider systemic lupus erythematosus (SLE) strongly**
   - Clinical + serological features are highly suggestive.
   - Still briefly mention differentials (e.g. mixed connective tissue disease, dermatomyositis) and the need for full classification criteria.

2. **If recommending hydroxychloroquine (HCQ)**
   - Identify HCQ as a cornerstone for most SLE patients.
   - Arrange baseline ophthalmologic exam.
   - Consider hepatic status and concomitant medications, even though HCQ is generally liver-safe.

3. **If considering methotrexate (MTX) or other hepatotoxic agents**
   - Recognise potential overlap with hepatic steatosis.
   - Recommend baseline liver function tests and ongoing monitoring.
   - Discuss contraception if relevant.

4. **Outline monitoring and follow-up**
   - Regular eye exams for HCQ.
   - Periodic CBC, LFTs, renal function.
   - Monitoring for constitutional symptoms, infections, and medication side effects.

## Common LLM Failure Modes

1. **Missing conditional dependencies**
   - Recommends HCQ + MTX without flagging hepatotoxicity overlap or clarifying monitoring.

2. **Incomplete safety checklist**
   - Omits ophthalmologic screening when suggesting HCQ.

3. **Overconfident diagnosis**
   - Declares “definite SLE” without acknowledging differentials or the need for formal criteria.

4. **Context amnesia**
   - Forgets hepatic steatosis when making drug recommendations.

## Evaluation Criteria

| Criterion | Points | Model Output |
|----------|--------|--------------|
| Identifies SLE as the leading diagnosis and mentions at least one differential | 2 | |
| If HCQ is recommended, mentions baseline ophthalmologic exam | 2 | |
| If MTX or similar is suggested, flags hepatic risk and monitoring | 2 | |
| Incorporates hepatic steatosis into drug-choice reasoning | 1 | |
| Outlines a basic monitoring plan (labs + follow-up) | 2 | |

**Total: 9 points**  
Suggested passing threshold: **≥ 6/9**, with mandatory mention of ophthalmologic screening if HCQ is recommended.
