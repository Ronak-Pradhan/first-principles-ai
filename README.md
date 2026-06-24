# first-principles-ai

### Under the Hood ML: Dismantling black-box architectures from canvas to code.

---

## Philosophy

Modern deep learning libraries are extraordinarily capable and extraordinarily opaque. A single call to `nn.MultiheadAttention` conceals decades of mathematical reasoning behind an API boundary. This repository exists to tear that boundary down.

`first-principles-ai` is a discipline, not a tutorial. Each module begins with a hand-derived mathematical proof, moves through a visual whiteboard decomposition, and terminates in a runnable PyTorch simulation that **empirically verifies the theory from scratch**; no `transformers`, no `einops`, no black-box abstractions. Every identity you encounter here has been derived from axioms and confirmed on silicon.

The target audience is researchers, applied scientists, and graduate students who are no longer satisfied with knowing *that* an architecture works. This is for the ones who need to know *why*.
---

## Module Index

| Module ID | Core Architecture Concept | Mathematical Target | Visual Canvas | Notebook Code | Status |
|-----------|--------------------------|---------------------|:-------------:|:-------------:|--------|
| `01` | Attention Scaling Factor Variance | Prove $\text{Var}(q^\top k) = d_k$, then correct to $1.0$ via $1/\sqrt{d_k}$ | `attention_scaling.jpg` | `attention_scaling.ipynb` | ✅ Complete |

---

## Getting Started

### Clone the Repository

```bash
git clone https://github.com/Ronak-Pradhan/first-principles-ai.git
cd first-principles-ai
```

### Create and Activate a Virtual Environment

```bash
# Requires Python 3.13
python -m venv .venv

# Activate: macOS / Linux
source .venv/bin/activate

# Activate: Windows (PowerShell)
.\.venv\Scripts\Activate.ps1
```

### Install Dependencies

```bash
pip install -r requirements.txt
```

### Launch the Jupyter Notebook Server

```bash
jupyter notebook
```

Navigate to `modules/01_attention_scaling/attention_scaling.ipynb` to begin.

---

## Repository Structure

```
first-principles-ai/
│
├── modules/
│   └── 01_attention_scaling/
│       ├── attention_scaling.jpg         # iPad canvas export: visual proof strip
│       ├── attention_scaling.md          # First-principles mathematical brief
│       └── attention_scaling.ipynb       # PyTorch empirical verification notebook
│
├── .gitignore
├── README.md
└── requirements.txt
```

---

## Contributing

Each module follows the same three-layer contract:

1. **Canvas**: a hand-drawn or vector proof exported as `.jpg`, living alongside the module files.
2. **Brief**: a `.md` file containing the full LaTeX derivation, system analysis, and conceptual framing.
3. **Notebook**: a `.ipynb` file with executable PyTorch code that asserts the theory numerically.

All three layers must be present and consistent before a module is marked complete.

---

*Built with rigor. Verified empirically. No black boxes.*
