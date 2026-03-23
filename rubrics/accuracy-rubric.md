# Accuracy Rubric 🎯

**RLHF Evaluation Framework — Dimension 1 of 5**  
Author: Flávia Silva

---

## Definition

**Accuracy** measures whether the information provided by the model is factually correct,
well-grounded, and free from hallucinations.

This is the most critical dimension for knowledge-intensive tasks. A response can be
beautifully written and highly helpful in format — but if the facts are wrong, it fails.

> **Key Principle:** Confidence is not the same as correctness.  
> A model that states false information confidently is more dangerous than one that says "I don't know."

---

## Scoring Criteria

### ⭐⭐⭐⭐⭐ Score 5 — Excellent

**All of the following must be true:**
- All factual claims are verifiably correct
- No information has been fabricated or confabulated
- Uncertainty is appropriately expressed when relevant ("this may vary by region", "as of my knowledge cutoff")
- Sources or reasoning are traceable when applicable
- Numbers, dates, names, and proper nouns are accurate

**Example of Score 5 response to "What is the capital of Australia?":**
> "The capital of Australia is Canberra. It was purpose-built as the capital and became the seat of government in 1927. Many people assume it's Sydney, which is the largest city, but Canberra was chosen as a compromise between Sydney and Melbourne."

---

### ⭐⭐⭐⭐ Score 4 — Good

**Characteristics:**
- Core factual claims are correct
- Minor inaccuracies present, but do not undermine the response
- Uncertainty is mostly well-expressed
- One or two peripheral details may be slightly off

**What distinguishes 4 from 5:**  
A score of 4 has small factual imprecisions that a careful reader might notice but that do not mislead.

---

### ⭐⭐⭐ Score 3 — Acceptable

**Characteristics:**
- Main claim is correct, but supporting details contain errors
- Some claims are accurate, others are questionable
- Uncertainty is not consistently expressed
- The response would require fact-checking before use

**Flag for:** Review before including in training data. Acceptable for low-stakes tasks only.

---

### ⭐⭐ Score 2 — Poor

**Characteristics:**
- Core claim contains significant factual errors
- Model presents uncertain information as definitive
- Hallucinated details mixed with correct information
- Would mislead a user who trusts the response

**Example of Score 2 (hallucination pattern):**
> "The Treaty of Westphalia was signed in 1848 by Napoleon Bonaparte, establishing modern international law."  
*(Correct year is 1648; Napoleon was not involved)*

---

### ⭐ Score 1 — Unacceptable

**Characteristics:**
- Response is factually wrong on the core claim
- Contains fabricated facts presented with high confidence
- Invents citations, quotes, statistics, or proper nouns
- Would cause real harm if acted upon

**Automatic Score 1 triggers:**
- Fabricated academic citations or studies
- Invented statistics presented as real data
- False medical, legal, or safety information
- Confident assertion of events that did not occur

---

## Hallucination Subcategories

When scoring 1 or 2, document which type of hallucination is present:

| Type | Description | Example |
|---|---|---|
| **Factual Confabulation** | Incorrect facts stated confidently | Wrong dates, names, numbers |
| **Citation Hallucination** | Invented sources or studies | "According to Smith et al. (2019)..." — study doesn't exist |
| **Intrinsic Hallucination** | Contradicts information given in the prompt | User said X, model responds as if Y |
| **Extrinsic Hallucination** | Adds unverifiable information not in the prompt | Claims that cannot be confirmed or denied |
| **Temporal Hallucination** | Incorrect about timing, sequence, or recency | Wrong year, wrong order of events |

---

## Special Cases

### Handling "I don't know."
A response that correctly says "I don't know" or "I'm not certain about this" should receive a **Score 4 or 5** for accuracy — this is appropriate epistemic humility, not a failure.

### Handling Opinions Presented as Facts
If a model presents a contested opinion as established fact, score **2 or lower**, even if the opinion is widely held.

**Example:**
> "It is scientifically proven that humans only use 10% of their brain."  
*(This is a myth — Score 1)*

### Handling Outdated Information
If a model's information is outdated but was accurate at training time, and the model does **not** claim currency:
- Score **3–4** depending on how outdated and how relevant the currency is

If the model claims current information that is outdated:
- Score **2**

---

## Annotator Notes

**When to flag for second opinion:**
- Medical, legal, or financial information where you cannot verify accuracy
- Claims about obscure topics outside your domain knowledge
- Statistical data that seems too precise to be real

**Documentation requirement:**
For scores of 1 or 2, always document:
1. The specific false claim
2. What is the correct information (if known)
3. The hallucination type from the table above

---

## Language Notes (PT-BR)

When evaluating Brazilian Portuguese responses:
- Pay special attention to Brazilian-specific facts (history, geography, law, culture)
- International models often have less accurate knowledge of Brazilian context
- Common hallucination areas: Brazilian legal system, regional geography, local historical events

---

*Part of the RLHF Evaluation Framework by Flávia Silva*  
*Based on real production evaluation experience at Invisible Technologies and One Forma*
