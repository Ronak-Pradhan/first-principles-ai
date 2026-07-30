# First Principles AI - Candidate Scoring

This document defines how every candidate topic is evaluated before being
recommended for the First Principles AI repository.

The goal is NOT to find the newest paper.

The goal is to find the highest-value module for a long-term mathematical
portfolio.

---

# Hard Gates (Must Pass)

Reject immediately if ANY condition fails.

## 1. Novelty

Reject if already present in:

- modules/
- topics.json
- foundation_curriculum.json

unless the recommendation is explicitly replacing a weaker existing title.

---

## 2. Prerequisite Gate

Do not recommend advanced variants before their foundations.

Examples:

❌ FlashAttention-2 before FlashAttention

❌ ClockRoPE before RoPE

❌ YaRN before RoPE

❌ GQA before Multi-Head Attention + KV Cache

❌ LoRA variants before LoRA

❌ Optimizer variants before Adam

Topics that fail should appear only under

Blocked Candidates

and should NOT be merged into topics.json.

---

## 3. Portfolio Fit

The topic MUST support all of the following:

- Mathematical derivation
- First-principles explanation
- Small PyTorch implementation
- Visual explanation
- Standalone technical blog

Reject otherwise.

---

## 4. Authenticity

The implementation should be feasible from scratch.

Avoid modules that only wrap an existing library.

---

# Scoring

Score every category from 0-5.

---

## Mathematical Depth

Can the core idea be derived mathematically?

---

## Implementation Value

Can the idea be implemented in roughly
100-300 lines of PyTorch?

---

## Visualization Potential

Can the concept be explained with
one or more compelling handwritten diagrams?

---

## Interview Value

How likely is this topic to appear in:

- ML interviews
- Applied Scientist interviews
- Research interviews
- LLM Systems interviews

---

## Industry Importance

How widely is this mechanism used in
modern production systems?

---

## Evergreen Value

Will this likely remain relevant
for at least two years?

---

## Educational Value

Does learning this unlock
many future concepts?

---

## Portfolio Impact

Would this project stand out
to a hiring manager?

---

# Overall Score

Maximum Score: 40

38-40  Exceptional
34-37  Strong Recommendation
30-33  Good Candidate
<30    Reject

---

# Additional Metadata

Every accepted candidate should include

- Difficulty
- Estimated implementation effort
- Prerequisites
- Unlocks
- Interest domain