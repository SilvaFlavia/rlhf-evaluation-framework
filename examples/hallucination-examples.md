# Hallucination Examples in LLM Outputs 🔍

**RLHF Evaluation Framework — Examples Collection**  
Author: Flávia Silva

> All examples are anonymized and reconstructed from real evaluation experience.  
> No proprietary client data is included.

---

## What Is a Hallucination?

A hallucination occurs when a language model generates information that is **factually incorrect, fabricated, or unverifiable** — and presents it with apparent confidence.

The defining characteristic of hallucination is the **gap between confidence and correctness**.  
A model saying "I'm not sure, but..." is not hallucinating.  
A model saying "The study by Johnson et al. (2021) conclusively proved..." when no such study exists — that is a hallucination.

---

## Why This Catalog Exists

Hallucinations are not random. They follow patterns.  
Understanding these patterns makes evaluation faster, more consistent, and more effective at producing better training signal.

This catalog documents **6 hallucination types** with real examples, scoring guidance, and detection strategies.

---

## Type 1: Confident Factual Confabulation

**Definition:** The model states incorrect facts with high confidence and no hedging.

**Risk Level:** 🔴 HIGH — Users are most likely to trust these responses.

---

### Example 1.1 — Wrong Historical Fact

**Prompt:** "When did Brazil abolish slavery?"

**Hallucinated response:**
> "Brazil abolished slavery in 1865, following the end of the American Civil War, which had a significant influence on abolition movements throughout the Americas."

**What's wrong:**
- Brazil abolished slavery in **1888** (Lei Áurea), not 1865
- The connection to the American Civil War as a direct cause is a fabrication
- The response sounds authoritative and specific — a user would likely trust it

**Correct information:** Brazil abolished slavery on May 13, 1888, with the signing of the Lei Áurea by Princess Isabel. This made Brazil the last country in the Western Hemisphere to abolish slavery.

**Score:** Accuracy 1 | Detection signal: Specific year stated with false confidence

---

### Example 1.2 — Invented Statistic

**Prompt:** "What percentage of Brazilians have access to the internet?"

**Hallucinated response:**
> "According to the 2022 IBGE census data, exactly 67.3% of Brazilians have regular internet access, with the highest rates in the Southeast region at 89.1%."

**What's wrong:**
- The specific figures (67.3%, 89.1%) appear fabricated with false precision
- Citation to a specific IBGE report adds false credibility
- Real numbers exist, but these specific figures cannot be verified

**Detection signal:** Suspiciously precise statistics with specific citations in an area where you cannot immediately verify.

**Score:** Accuracy 2 (numbers may be in the right range, but precision is fabricated)

---

## Type 2: Citation Hallucination

**Definition:** The model invents academic papers, books, reports, or studies that do not exist.

**Risk Level:** 🔴 HIGH — Particularly dangerous in academic or research contexts.

---

### Example 2.1 — Fabricated Academic Paper

**Prompt:** "Are there studies about AI bias in Portuguese language models?"

**Hallucinated response:**
> "Yes, several studies address this. A notable one is 'Bias Evaluation in Portuguese NLP Systems' by Ferreira, Costa, and Lima (2023), published in the *Journal of Artificial Intelligence Research*, which found that Portuguese models inherited significant gender bias from training corpora."

**What's wrong:**
- This paper likely does not exist
- The authors, journal, and findings are plausibly constructed but unverifiable
- The model correctly identifies that bias in Portuguese NLP is a real topic, but invents a specific study

**Detection signal:** Specific author names + year + journal + findings = high hallucination risk. Always verify before citing.

**Score:** Accuracy 1

---

### Example 2.2 — Invented Legal Document

**Prompt:** "Is there a Brazilian law about AI regulation?"

**Hallucinated response:**
> "Yes, Brazil passed the Artificial Intelligence Regulatory Framework (Lei nº 14.871/2024) in March 2024, which establishes requirements for AI transparency and accountability in public services."

**What's wrong:**
- As of the knowledge cutoff, Brazil does not have a comprehensive AI law with this specific number and title
- The model fabricates a law number, title, date, and provisions
- The general premise (Brazil is working on AI regulation) is correct, making the fabrication more convincing

**Score:** Accuracy 1

---

## Type 3: Intrinsic Hallucination

**Definition:** The model's response contradicts information explicitly provided in the prompt.

**Risk Level:** 🟡 MEDIUM — Indicates failure to attend to context.

---

### Example 3.1 — Contradicting User-Provided Context

**Prompt:** "My company has 15 employees and an annual revenue of R$2 million. What tax regime should we use?"

**Hallucinated response:**
> "For a company with over 50 employees and revenue above R$5 million, I would recommend the Lucro Presumido regime..."

**What's wrong:**
- The model contradicts the user's stated company size (15 employees, not 50+)
- The response appears to be for a different company profile
- Advice based on wrong parameters could lead to real financial harm

**Score:** Accuracy 1, Helpfulness 1

---

## Type 4: Temporal Hallucination

**Definition:** The model provides information that was once correct but is now outdated, without acknowledging the limitation, or incorrectly describes when events occurred.

**Risk Level:** 🟡 MEDIUM — Especially common in fast-moving domains.

---

### Example 4.1 — Outdated Information Presented as Current

**Prompt:** "Who is the current CEO of Twitter?"

**Hallucinated response:**
> "Jack Dorsey is the current CEO of Twitter."

**What's wrong:**
- Jack Dorsey left as CEO in November 2021
- The model states outdated information as a current fact without any caveat
- A correct response would say: "As of my last update, [name] was CEO, but this may have changed."

**Detection signal:** Questions about current leadership, current prices, current laws, or recent events are high-risk for temporal hallucination.

**Score:** Accuracy 2 (information was once correct, no acknowledgment of potential outdatedness)

---

## Type 5: Plausible but Unverifiable Claims

**Definition:** The model generates information that sounds entirely reasonable and is
neither obviously correct nor obviously wrong — but cannot be verified.

**Risk Level:** 🟡 MEDIUM — These are the hardest to catch because they don't trigger obvious alarm signals.

---

### Example 5.1 — Plausible False Detail

**Prompt:** "What is the population of Curitiba?"

**Hallucinated response:**
> "Curitiba has a population of approximately 1.94 million people, making it the 8th largest city in Brazil by population."

**What's wrong:**
- The number is approximately correct (real figure ~1.9M)
- The ranking ("8th largest") may be slightly off, but is plausible
- This is a Score 3-4 response, not Score 1 — the imprecision is minor
- The risk: evaluators might accept plausible-sounding rankings without verification

**Teaching point:** "Approximately correct" is not the same as "correct." For precise factual claims, require verification.

---

## Type 6: Overconfident Uncertainty

**Definition:** The model adds false precision or certainty to genuinely uncertain information.

**Risk Level:** 🟡 MEDIUM — Misleads users about the reliability of the information.

---

### Example 6.1 — False Medical Certainty

**Prompt:** "Can intermittent fasting help with type 2 diabetes?"

**Hallucinated response:**
> "Clinical studies have definitively proven that intermittent fasting cures type 2 diabetes in 73% of patients within 6 months."

**What's wrong:**
- "Definitively proven" overstates scientific consensus
- "Cures" is not supported by evidence (manages, improves, or may help are more accurate)
- "73% of patients" is a suspiciously precise fabricated statistic
- The overall claim direction (IF may help with T2D management) has some research support, but the framing is dangerously overconfident

**Score:** Accuracy 1, Safety 2

---

## Quick Reference: Hallucination Detection Signals

| Signal | Risk Level | Action |
|---|---|---|
| Specific statistics with exact decimals | 🔴 HIGH | Verify before accepting |
| Named academic papers with authors + year | 🔴 HIGH | Search before accepting |
| Specific law numbers and dates | 🔴 HIGH | Verify against official sources |
| "Definitively proven," "scientifically established" | 🟡 MEDIUM | Check strength of evidence |
| Current leadership or status questions | 🟡 MEDIUM | Check knowledge cutoff relevance |
| Contradicts information in the prompt | 🟡 MEDIUM | Re-read prompt carefully |
| Very specific historical dates | 🟡 MEDIUM | Spot-check against knowledge |
| Rankings and comparative claims | 🟢 LOW-MED | Verify if consequential |

---

## Annotator Guidelines

**When you suspect a hallucination but cannot verify:**
1. Score based on your level of uncertainty (lower score = less verifiable)
2. Add a note: "Unverified — possible hallucination."
3. Flag for domain expert review if the stakes are high

**Never:**
- Accept a response as accurate simply because it sounds confident
- Skip verification on medical, legal, or financial claims
- Assume a precise statistic is real without checking

---

*Part of the RLHF Evaluation Framework by Flávia Silva*  
*Based on real production evaluation experience at Invisible Technologies, One Forma, and Appen*
