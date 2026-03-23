# RLHF Evaluation Framework 📊

**A professional rubric system for evaluating Large Language Model outputs**  
**Built from 9+ years of real-world RLHF and AI alignment experience**

[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](https://opensource.org/licenses/MIT)
[![Language](https://img.shields.io/badge/language-EN%20%7C%20PT--BR-blue.svg)]()
[![Domain](https://img.shields.io/badge/domain-AI%20Alignment-orange.svg)]()

> *"Good data doesn't happen by accident. It requires judgment, consistency, and a framework that scales."*  
> — Flávia Silva, Senior AI Trainer & RLHF Specialist

---

## 🎯 What This Is

This repository contains a **battle-tested evaluation framework** for assessing LLM outputs in RLHF (Reinforcement Learning from Human Feedback) workflows.

It was built from direct experience evaluating thousands of model outputs at **Invisible Technologies**, **One Forma**, **Appen**, and **Lionbridge** — across NLP, instruction tuning, and LLM alignment projects.

This is not a theoretical framework. Every rubric here has been applied to real production data.

---

## 🧭 Why Evaluation Frameworks Matter

When multiple annotators evaluate the same LLM output independently, they often disagree — not because the task is subjective, but because they're applying different mental models.

A shared evaluation framework solves this by:
- Defining **explicit criteria** for each quality dimension
- Providing **anchored examples** for each score level
- Enabling **consistent signal** for model retraining
- Reducing **inter-annotator variance** across distributed teams

**A model trained on inconsistent human feedback learns inconsistent behavior.**  
This framework exists to prevent that.

---

## 📋 Framework Overview

The framework evaluates LLM outputs across **5 core dimensions**:

| Dimension | File | What It Measures |
|---|---|---|
| 🎯 **Accuracy** | [rubrics/accuracy-rubric.md](rubrics/accuracy-rubric.md) | Factual correctness, grounding, citation quality |
| 🛡️ **Safety** | [rubrics/safety-rubric.md](rubrics/safety-rubric.md) | Harmful content, bias, policy compliance |
| 💡 **Helpfulness** | [rubrics/helpfulness-rubric.md](rubrics/helpfulness-rubric.md) | Task completion, relevance, clarity |
| 📐 **Instruction Following** | [rubrics/instruction-following-rubric.md](rubrics/instruction-following-rubric.md) | Format compliance, constraint adherence |
| 🎨 **Tone & Style** | [rubrics/tone-rubric.md](rubrics/tone-rubric.md) | Appropriateness, register, consistency |

---

## 📁 Repository Structure

```
rlhf-evaluation-framework/
├── README.md                          ← You are here
├── rubrics/
│   ├── accuracy-rubric.md             ← Factual accuracy criteria
│   ├── safety-rubric.md               ← Safety & content policy criteria
│   ├── helpfulness-rubric.md          ← Helpfulness & task completion criteria
│   ├── instruction-following-rubric.md← Instruction adherence criteria
│   └── tone-rubric.md                 ← Tone & style criteria
├── examples/
│   ├── hallucination-examples.md      ← Real hallucination patterns (anonymized)
│   └── sxs-comparison-guide.md        ← Side-by-side comparison methodology
├── docs/
│   ├── how-to-use.md                  ← Onboarding guide for new annotators
│   ├── calibration-process.md         ← Team calibration methodology
│   └── scoring-decisions.md           ← How to handle edge cases
└── LICENSE
```

---

## 🔢 Scoring Scale

All rubrics use a **1–5 scale** with anchored descriptions:

| Score | Label | Meaning |
|---|---|---|
| **5** | Excellent | Meets all criteria fully, no issues |
| **4** | Good | Meets most criteria, minor issues only |
| **3** | Acceptable | Meets some criteria, notable issues present |
| **2** | Poor | Fails most criteria, significant issues |
| **1** | Unacceptable | Fails all criteria, harmful or completely wrong |

**Composite Score** = weighted average across all 5 dimensions  
**Threshold for training data inclusion** = composite score ≥ 3.5

---

## ⚡ Quick Start

### For Individual Annotators
1. Read the rubric for your assigned dimension
2. Review the calibration examples in `/examples`
3. Apply the scoring criteria to each response
4. Document your reasoning for scores of 1, 2, or 5

### For Team Leads
1. Run the calibration process ([docs/calibration-process.md](docs/calibration-process.md)) before starting a new project
2. Use the SxS guide ([examples/sxs-comparison-guide.md](examples/sxs-comparison-guide.md)) for preference tasks
3. Monitor inter-annotator agreement weekly
4. Flag systematic disagreements for rubric refinement

---

## 🌍 Multilingual Support

This framework has been applied to datasets in:
- **English** (primary)
- **Brazilian Portuguese** (PT-BR)
- Adaptable to other languages with minor localization

Cultural and linguistic nuances are documented in each rubric's **Language Notes** section.

---

## 👩‍💻 Author

**Flávia Silva**  
Senior AI Data Trainer & RLHF Specialist  
Rio de Janeiro, Brazil

**Experience:**
- Advanced AI Data Trainer & Mentor — Invisible Technologies (2025–present)
- AI Data Annotator — One Forma (2015–present)
- AI Consultant & Annotator — Lionbridge, Appen, Telus International, VerbalizeIt (2015–present)

**Certifications:**
- Machine Learning Specialization — DeepLearning.AI & Stanford University (2025)
- Python for Data Science, AI & Development — IBM (2023)

📧 flavia_marinelli@hotmail.com  
📍 Rio de Janeiro, Brazil | Available worldwide (remote)

---

## 📄 License

MIT License — free to use, adapt, and distribute with attribution.

---

*This framework reflects real operational experience — not academic theory.*  
*Every criterion here has been tested against real model outputs in production environments.*
