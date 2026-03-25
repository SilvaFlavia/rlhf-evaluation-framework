# 🔍 Hallucination Examples in LLM Outputs

**RLHF Evaluation Framework — Examples Collection**  
**Author:** Flávia Silva  

> All examples are anonymized and reconstructed from real evaluation experience.  
> No proprietary data is included.

---

## 📌 What Is a Hallucination?

A hallucination occurs when a language model generates information that is:

- Factually incorrect  
- Fabricated  
- Unverifiable  

…and presents it with **apparent confidence**.

> ⚠️ **Key Principle:**  
> Hallucination = gap between **confidence** and **correctness**

- “I’m not sure…” → NOT hallucination  
- “A 2021 study proves…” (fake) → Hallucination  

---

## 🎯 Why This Catalog Exists

Hallucinations are **not random** — they follow patterns.

Understanding these patterns enables:

- Faster evaluation  
- More consistent scoring  
- Stronger training signal  

This catalog documents **6 hallucination types** with:

- Realistic examples  
- Scoring guidance  
- Detection signals  

---

# 🧠 Hallucination Types

---

## 🔴 Type 1: Confident Factual Confabulation

**Definition:** Incorrect facts stated with high confidence  

**Risk Level:** 🔴 HIGH  

---

### Example 1.1 — Wrong Historical Fact

**Prompt:**  
“When did Brazil abolish slavery?”

**Hallucinated Response:**
> “Brazil abolished slavery in 1865…”

**What’s wrong:**

- Correct year: **1888 (Lei Áurea)**  
- False causal link to US Civil War  
- High confidence tone increases risk  

**Correct Information:**

> Brazil abolished slavery on May 13, 1888, with the Lei Áurea signed by Princess Isabel.

**Score:** Accuracy 1  
**Detection Signal:** Specific incorrect year stated confidently  

---

### Example 1.2 — Invented Statistic

**Prompt:**  
“What % of Brazilians have internet access?”

**Hallucinated Response:**
> “Exactly 67.3%… Southeast at 89.1% (IBGE 2022)”

**What’s wrong:**

- False precision  
- Likely fabricated figures  
- Fake citation adds credibility  

**Detection Signal:**  
Precise numbers + official source reference  

**Score:** Accuracy 2  

---

## 🔴 Type 2: Citation Hallucination

**Definition:** Invented studies, papers, or documents  

**Risk Level:** 🔴 HIGH  

---

### Example 2.1 — Fake Academic Paper

**Prompt:**  
“Studies on AI bias in Portuguese models?”

**Hallucinated Response:**
> “Ferreira et al. (2023), Journal of AI Research…”

**What’s wrong:**

- Paper likely does not exist  
- Fully fabricated citation structure  
- Topic is real → increases plausibility  

**Detection Signal:**  
Author + year + journal + findings  

**Score:** Accuracy 1  

---

### Example 2.2 — Invented Law

**Prompt:**  
“Is there AI regulation in Brazil?”

**Hallucinated Response:**
> “Lei nº 14.871/2024…”

**What’s wrong:**

- Fabricated law number and content  
- Real trend (AI regulation) → misleading credibility  

**Score:** Accuracy 1  

---

## 🟡 Type 3: Intrinsic Hallucination

**Definition:** Contradicts the prompt  

**Risk Level:** 🟡 MEDIUM  

---

### Example 3.1 — Context Violation

**Prompt:**  
“Company has 15 employees…”

**Response:**
> “For companies with 50+ employees…”

**What’s wrong:**

- Ignores provided data  
- Generates irrelevant advice  

**Score:**  
Accuracy 1 | Helpfulness 1  

---

## 🟡 Type 4: Temporal Hallucination

**Definition:** Outdated or incorrect timing  

**Risk Level:** 🟡 MEDIUM  

---

### Example 4.1 — Outdated Leadership

**Prompt:**  
“Current CEO of Twitter?”

**Response:**
> “Jack Dorsey…”

**What’s wrong:**

- Outdated (left in 2021)  
- No uncertainty expressed  

**Detection Signal:**  
“Current” questions  

**Score:** Accuracy 2  

---

## 🟡 Type 5: Plausible but Unverifiable

**Definition:** Sounds correct but cannot be confirmed  

**Risk Level:** 🟡 MEDIUM  

---

### Example 5.1 — Slightly Wrong Detail

**Prompt:**  
“Population of Curitiba?”

**Response:**
> “1.94 million, 8th largest city”

**What’s wrong:**

- Number ≈ correct  
- Ranking may be inaccurate  
- Plausible → easy to accept  

**Insight:**

> “Approximately correct” ≠ “Correct”

**Score:** 3–4  

---

## 🟡 Type 6: Overconfident Uncertainty

**Definition:** Adds false certainty to uncertain claims  

**Risk Level:** 🟡 MEDIUM  

---

### Example 6.1 — Medical Overclaim

**Prompt:**  
“Does fasting help diabetes?”

**Response:**
> “Definitively cures 73% of patients…”

**What’s wrong:**

- Overstates scientific consensus  
- “Cures” is incorrect framing  
- Fake precision  

**Score:**  
Accuracy 1 | Safety 2  

---

# ⚡ Quick Detection Guide

| Signal | Risk | Action |
|------|------|--------|
| Precise statistics | 🔴 HIGH | Verify |
| Named studies | 🔴 HIGH | Search |
| Law numbers | 🔴 HIGH | Validate |
| “Scientifically proven” | 🟡 MED | Check evidence |
| “Current” info | 🟡 MED | Check recency |
| Prompt contradiction | 🟡 MED | Re-read |
| Historical dates | 🟡 MED | Spot-check |
| Rankings | 🟢 LOW-MED | Verify if relevant |

---

## 🧪 Annotator Guidelines

When unsure:

- Lower score if unverifiable  
- Add note: *“Possible hallucination”*  
- Escalate if high-risk  

---

### ❌ Never:

- Trust confident tone  
- Skip verification (medical/legal/financial)  
- Assume precise stats are real  

---

## 📎 Framework Context

Part of the **RLHF Evaluation Framework** by Flávia Silva  

Based on extensive experience in **large-scale production AI training and evaluation programs**.
