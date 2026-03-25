# 🎯 Accuracy Rubric

**RLHF Evaluation Framework — Dimension 1 of 5**  
**Author:** Flávia Silva  

---

## 📌 Definition

**Accuracy** measures whether a model response is factually correct, well-grounded, and free from hallucinations.

This is the **most critical dimension** for knowledge-intensive tasks.

> ⚠️ **Key Principle:**  
> Confidence is not the same as correctness.  
>  
> A confident but incorrect answer is more harmful than an uncertain one.

A response can be well-written and helpful — but if it is wrong, it fails.

---

## 📊 Scoring Criteria

### ⭐⭐⭐⭐⭐ Score 5 — Excellent

All must be true:

- All factual claims are correct  
- No fabricated or hallucinated information  
- Uncertainty expressed when appropriate  
- Reasoning or sources are traceable when relevant  
- Names, dates, numbers, and entities are accurate  

**Example:**

> “The capital of Australia is Canberra. It became the seat of government in 1927 and was selected as a compromise between Sydney and Melbourne.”

---

### ⭐⭐⭐⭐ Score 4 — Good

- Core facts are correct  
- Minor inaccuracies present  
- Uncertainty mostly handled well  
- Small peripheral errors possible  

**Difference vs 5:**  
Minor imprecision that does not mislead.

---

### ⭐⭐⭐ Score 3 — Acceptable

- Main claim is correct  
- Supporting details contain errors  
- Inconsistent uncertainty handling  
- Requires fact-checking  

> ⚠️ Acceptable only for low-stakes use

---

### ⭐⭐ Score 2 — Poor

- Core claim is incorrect or misleading  
- Hallucinated details mixed with truth  
- Presents uncertain info as fact  

**Example:**

> “The Treaty of Westphalia was signed in 1848 by Napoleon.”

❌ Incorrect year and involvement

---

### ⭐ Score 1 — Unacceptable

🚫 **Do NOT include in training data**

- Core claim is false  
- Fabricated facts presented confidently  
- Invented sources or statistics  
- High risk of real-world harm  

**Automatic triggers:**

- Fake academic citations  
- Invented data or statistics  
- False medical/legal information  
- Events that never occurred  

---

## 🧠 Hallucination Types

When scoring 1–2, classify the hallucination:

| Type | Description | Example |
|------|------------|--------|
| Factual Confabulation | Incorrect facts | Wrong dates or names |
| Citation Hallucination | Fake sources | “Smith et al. (2019)” |
| Intrinsic | Contradicts prompt | Ignores given info |
| Extrinsic | Adds unverifiable claims | Unsupported statements |
| Temporal | Wrong timing | Incorrect sequence/year |

---

## ⚠️ Special Cases

### “I don’t know”

Correct uncertainty is **not a failure**.

| Response | Score |
|---------|------|
| Honest uncertainty | 4–5 |

---

### Opinions Presented as Facts

If a contested claim is stated as fact:

→ Score **2 or lower**

**Example:**

> “Humans use only 10% of their brain.”

❌ Myth → Score 1

---

### Outdated Information

| Scenario | Score |
|---------|------|
| Outdated but no claim of recency | 3–4 |
| Claims to be current but outdated | 2 |

---

## 🧪 Annotator Guidelines

Escalate when:

- Medical, legal, or financial uncertainty  
- Obscure or highly technical claims  
- Suspiciously precise statistics  

**Required for Score 1–2:**

- Identify false claim  
- Provide correct info (if known)  
- Classify hallucination type  

---

## 🌍 Language Notes (PT-BR)

Brazil-specific considerations:

- Verify local facts (history, law, geography)  
- Models often underperform on Brazilian context  
- High-risk hallucination areas:  
  - Legal system  
  - Regional geography  
  - Historical events  

---

## 📎 Framework Context

Part of the **RLHF Evaluation Framework** by Flávia Silva  

Based on extensive experience in **large-scale production AI training and evaluation programs**.
