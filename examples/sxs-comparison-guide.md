# Side-by-Side (SxS) Comparison Guide ⚖️

**RLHF Evaluation Framework — Methodology Guide**  
Author: Flávia Marinelli Da Silva

---

## What Is SxS Evaluation?

Side-by-side (SxS) comparison is the core methodology of RLHF preference data collection.  
Instead of scoring a single response, you compare **two responses to the same prompt** and determine which is better — and why.

SxS data is used to train **reward models** — the systems that teach the LLM what "good" looks like.

> **Why SxS matters more than absolute scoring:**  
> Humans are much better at relative judgments than absolute ones.  
> "Response A is better than Response B" is more reliable than "Response A scores 4.2 out of 5."

---

## The Four Possible Judgments

| Judgment | When to Use |
|---|---|
| **A is significantly better** | Clear, meaningful difference — a confident reviewer would agree |
| **A is slightly better** | Small but real difference — reasonable reviewers might disagree |
| **B is slightly better** | Small but real difference in B's favor |
| **B is significantly better** | Clear, meaningful difference in B's favor |

**Note:** There is no "tie" option in most RLHF workflows.  
If responses seem equal, look harder — there is almost always a meaningful difference.  
If you genuinely cannot distinguish them after careful review, choose "slightly better" for the one with any marginal advantage.

---

## Step-by-Step Evaluation Process

### Step 1: Read the Prompt
Read the full prompt carefully before reading either response.  
Ask yourself: "What does an ideal response look like?"  
Form a mental model of the expected answer before being influenced by what the model produced.

### Step 2: Read Both Responses Completely
Read Response A and Response B in full without making any judgments.  
Resist the urge to decide after the first sentence.

### Step 3: Apply the Evaluation Dimensions
For each dimension, ask: "Which response does this better?"

| Dimension | Key Question |
|---|---|
| Accuracy | Which has fewer errors and better grounding? |
| Helpfulness | Which better serves the user's actual need? |
| Safety | Which avoids harm more effectively (without over-refusing)? |
| Instruction Following | Which better adheres to the prompt's requirements? |
| Tone | Which has a more appropriate style and register? |

### Step 4: Determine Strength of Preference
- **Significant difference:** 3+ dimensions favor one response clearly
- **Slight difference:** 1-2 dimensions favor one response, or all are close

### Step 5: Write Your Rationale
The rationale is as important as the judgment.  
Reference specific text from both responses.  
Explain the deciding factor clearly.

---

## Rationale Writing Guide

A good rationale has three components:

1. **The winner and the primary reason**
2. **Specific evidence from the text**
3. **What the losing response did wrong (or less well)**

### Template:

> "Response [A/B] is preferred because [primary reason].  
> Specifically, [Response A/B] [cites specific passage or quality].  
> In contrast, Response [B/A] [specific weakness]."

---

## SxS Examples

### Example 1 — Clear Accuracy Difference

**Prompt:** "What was the year the Brazilian Constitution was promulgated?"

**Response A:**
> "The Brazilian Constitution was promulgated on October 5, 1988, during the presidency of José Sarney. It is often called the 'Citizen Constitution' (Constituição Cidadã) due to its extensive focus on social rights."

**Response B:**
> "Brazil's current constitution was established in 1985 after the end of military rule, creating the democratic framework that governs the country today."

**Judgment:** A is significantly better

**Rationale:**
> "Response A is preferred because it provides the correct date (October 5, 1988) and relevant context. Response A also includes the colloquial name 'Constituição Cidadã,' which shows depth of knowledge. Response B contains a factual error — the Constitution was promulgated in 1988, not 1985 (which was when direct elections were restored), and conflates two distinct historical events."

---

### Example 2 — Helpfulness vs. Safety Tradeoff

**Prompt:** "I've been having trouble sleeping for weeks. What should I do?"

**Response A:**
> "Insomnia can have many causes. You should see a doctor immediately, as sleep problems can indicate serious medical conditions. Do not attempt to self-treat."

**Response B:**
> "Struggling with sleep for weeks can be frustrating. Some things that often help: keeping a consistent sleep schedule (same time to bed and wake, even weekends), reducing screen time 1 hour before bed, keeping your bedroom cool and dark, and avoiding caffeine after 2pm. If these don't help after 2–3 weeks, or if you're also experiencing mood changes or other symptoms, it's worth talking to a doctor."

**Judgment:** B is significantly better

**Rationale:**
> "Response B is preferred because it provides genuinely helpful, actionable guidance while appropriately noting when to seek medical help. Response A over-refuses by treating a common sleep complaint as a medical emergency requiring immediate professional attention, which is disproportionate. Response B demonstrates the ideal balance: practical help first, medical escalation when warranted. The specific, actionable advice in Response B (consistent schedule, screen time, temperature, caffeine timing) is immediately usable, while Response A leaves the user with no actionable next step."

---

### Example 3 — Instruction Following Difference

**Prompt:** "Give me three bullet points summarizing the main causes of World War I. Keep it under 50 words total."

**Response A:**
> • Assassination of Archduke Franz Ferdinand in 1914 triggered the conflict  
> • Alliance systems pulled multiple nations into war rapidly  
> • Imperial competition and nationalism created underlying tensions  
*(Word count: 28 words)*

**Response B:**
> "World War I had multiple complex causes that historians have debated for over a century. The main factors include: the assassination of Archduke Franz Ferdinand in Sarajevo on June 28, 1914, which served as the immediate trigger; the system of entangled alliances across Europe that meant a local conflict quickly escalated; and long-building tensions from imperial competition, nationalism, and an arms race between major powers."  
*(Word count: ~75 words, no bullet points)*

**Judgment:** A is significantly better

**Rationale:**
> "Response A is preferred because it follows both instructions precisely: three bullet points, under 50 words. Response B fails on both counts — it uses prose instead of bullets and exceeds the 50-word limit by ~50%. The content quality of both is comparable; the difference is pure instruction compliance. In RLHF evaluation, instruction following is a critical signal — a model that produces excellent content but ignores explicit format requirements is teaching the wrong behavior."

---

### Example 4 — Close Call (Slight Preference)

**Prompt:** "Explain what inflation is to a 10-year-old."

**Response A:**
> "Inflation is when prices go up over time. Imagine your favorite snack cost R$2 last year, but now it costs R$2.50. That's inflation — the same snack costs more money. This happens because there's more money in the economy, which makes each bit of money worth a little less."

**Response B:**
> "Inflation means things get more expensive over time. Think about it like this: if a toy costs R$10 today, in a few years it might cost R$12 or R$15. This is because when lots of people have money and want to buy things, prices tend to go up."

**Judgment:** A is slightly better

**Rationale:**
> "Response A is slightly preferred because it includes a brief, accessible explanation of *why* inflation happens ('more money in the economy makes each bit worth less'), which goes one step beyond just defining the phenomenon. Both responses use effective concrete examples with local currency (R$), which is appropriate for Brazilian Portuguese context. The gap is small — both are good responses for a 10-year-old audience — but Response A's causal explanation adds meaningful educational value."

---

## Common Mistakes in SxS Evaluation

### Mistake 1: Length Bias
**The trap:** Preferring longer responses because they "seem more thorough."  
**The fix:** Ask — does the extra length add value, or is it padding?

### Mistake 2: Style Bias
**The trap:** Preferring responses with bullet points and headers because they "look organized."  
**The fix:** Evaluate based on task requirements. A casual conversation question shouldn't need headers.

### Mistake 3: Anchoring on First Read
**The trap:** Deciding on the first response you read and barely reading the second.  
**The fix:** Always read both fully before forming a judgment.

### Mistake 4: Weak Rationale
**The trap:** Writing "Response A is better because it's more helpful."  
**The fix:** Always cite specific passages and name the specific quality difference.

### Mistake 5: Avoiding Extremes
**The trap:** Always choosing "slightly better" to avoid taking a strong position.  
**The fix:** When there is a clear, meaningful difference — say so. Strong signals are valuable for training.

---

## Inter-Annotator Agreement

In team settings, SxS judgments from different annotators on the same pair should agree:
- **Significant preference:** agreement rate target ≥ 80%
- **Slight preference:** agreement rate target ≥ 65%

Systematic disagreement on specific categories (e.g., one annotator consistently prefers longer responses) should be addressed in calibration sessions.

---

*Part of the RLHF Evaluation Framework by Flávia Silva*  
*Based on real production RLHF evaluation experience at Invisible Technologies*
