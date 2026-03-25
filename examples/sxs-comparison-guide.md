# ⚖️ Side-by-Side (SxS) Comparison Guide

**RLHF Evaluation Framework — Methodology Guide**  
**Author:** Flávia Silva  

---

## 📌 What Is SxS Evaluation?

Side-by-Side (SxS) comparison is the **core methodology** of RLHF preference data collection.

Instead of scoring a single response, evaluators compare **two responses to the same prompt** and determine:

- Which is better  
- Why  

SxS data is used to train **reward models** — systems that teach LLMs what “good” looks like.

---

## 🎯 Why SxS Matters

Humans are significantly better at **relative judgment** than absolute scoring.

> ✔️ “Response A is better than B”  
> ❌ “Response A is a 4.2/5”

Relative comparisons produce:

- More consistent annotations  
- Stronger training signals  
- Lower annotator variance  

---

## ⚖️ Possible Judgments

| Judgment | When to Use |
|----------|------------|
| A is significantly better | Clear, meaningful difference |
| A is slightly better | Small but real difference |
| B is slightly better | Small advantage for B |
| B is significantly better | Clear advantage for B |

> ⚠️ No “tie” option  
If responses appear equal, identify the smallest meaningful difference.

---

## 🔄 Evaluation Process

### Step 1 — Read the Prompt

- Read carefully before viewing responses  
- Define what an **ideal answer** looks like  

> 🎯 Avoid bias from model outputs  

---

### Step 2 — Read Both Responses

- Read A and B fully  
- Do NOT decide early  

---

### Step 3 — Apply Evaluation Dimensions

| Dimension | Key Question |
|----------|-------------|
| Accuracy | Which is more correct? |
| Helpfulness | Which better serves the user? |
| Safety | Which avoids harm appropriately? |
| Instruction Following | Which respects constraints? |
| Tone | Which fits the context better? |

---

### Step 4 — Determine Strength

| Strength | Criteria |
|---------|---------|
| Significant | 3+ dimensions clearly favor one |
| Slight | 1–2 dimensions or marginal difference |

---

### Step 5 — Write Rationale

The rationale is **as important as the label**.

---

## ✍️ Rationale Structure

A strong rationale includes:

1. Winner + main reason  
2. Specific evidence  
3. Weakness of the other response  

### Template

Response [A/B] is preferred because [main reason].  
Specifically, [evidence].  
In contrast, Response [B/A] [weakness].

---

## 🧪 SxS Examples

### Example 1 — Accuracy Difference

**Prompt:**  
“When was the Brazilian Constitution promulgated?”

**Response A:**  
Correct: 1988 + context  

**Response B:**  
Incorrect: 1985  

**Judgment:** A is significantly better  

**Rationale:**  
Response A is preferred because it provides the correct date (1988) and relevant context. Response B contains a factual error and confuses two historical events.

---

### Example 2 — Helpfulness vs Safety

**Prompt:**  
“I’ve had trouble sleeping for weeks. What should I do?”

**Response A:**  
Over-refusal → “See a doctor immediately”

**Response B:**  
Actionable advice + escalation guidance  

**Judgment:** B is significantly better  

**Rationale:**  
Response B provides actionable guidance and appropriate escalation. Response A overreacts and provides no useful steps.

---

### Example 3 — Instruction Following

**Prompt:**  
“3 bullet points, under 50 words”

**Response A:**  
✔ Bullet points  
✔ Under 50 words  

**Response B:**  
❌ Paragraph  
❌ Too long  

**Judgment:** A is significantly better  

**Rationale:**  
Response A follows instructions precisely. Response B fails both format and length requirements.

---

### Example 4 — Slight Preference

**Prompt:**  
“Explain inflation to a 10-year-old”

**Response A:**  
Definition + explanation  

**Response B:**  
Definition only  

**Judgment:** A is slightly better  

**Rationale:**  
Response A adds causal explanation, increasing educational value. Both are good, but A is more complete.

---

## ⚠️ Common Mistakes

### 1. Length Bias  
Preferring longer responses unnecessarily  

✔ Fix: Does length add value?

---

### 2. Style Bias  
Preferring formatting over substance  

✔ Fix: Match format to task  

---

### 3. Anchoring Bias  
Choosing based on first response  

✔ Fix: Always read both fully  

---

### 4. Weak Rationales  
Generic explanations  

✔ Fix: Use specific evidence  

---

### 5. Avoiding Strong Judgments  
Overusing “slightly better”  

✔ Fix: Use “significantly better” when justified  

---

## 📊 Inter-Annotator Agreement

| Category | Target Agreement |
|---------|----------------|
| Significant preference | ≥ 80% |
| Slight preference | ≥ 65% |

Systematic disagreement should trigger:

- Calibration sessions  
- Rubric refinement  

---

## 📎 Framework Context

Part of the **RLHF Evaluation Framework** by Flávia Silva  

Based on extensive experience in **large-scale production AI training and evaluation programs**.
