# Weekly AI Math Digest (2026-W31)

_Generated 2026-07-30. Sources: `foundation_curriculum.json` gap rank; venue proceedings (EMNLP / NeurIPS / ICLR / ICML); Google DeepMind Gemma 2 tech report; lab pages best-effort. X lookups blocked this run (expected) - skipped._

## Suggested next module

**Softmax Backpropagation & Full Jacobian Matrix Derivation** (`softmax_jacobian`, curriculum `f02`, backlog `02`).

Only `modules/01_attention_scaling` has three-layer evidence (brief + canvas + notebook). Softmax is the immediate operator after the scaled logits that module justifies, and it is already queued as a manual foundation topic. Prefer shipping this spine item over new papers while modules `02`-`10` are largely still todo.

**Prerequisites already satisfied:** scaled attention logits and the \(1/\sqrt{d_k}\) variance story (module 01); softmax as the attention normalizer used in that module; basic chain-rule / backprop fluency expected for the portfolio format.

## Foundation gaps

Uncovered curriculum classics (no matching backlog slug / not three-layer shipped), ranked for interview usefulness, industry longevity, math depth, portfolio value, and soft prereq readiness after attention scaling:

1. **Multi-head attention as partitioned subspaces** (`f09`) - Direct architectural sequel to scaled dot-product; \(d_k = d_{\mathrm{model}}/h\) interview staple; prereq `attention_scaling` satisfied.
2. **Causal / attention mask structure** (`f08`) - Additive \(-\infty\) before softmax; decoder legality; soft-ready once softmax Jacobian is underway.
3. **Residual connections as identity gradient highways** (`f07`) - Universal depth-stability identity; high longevity across CNNs and transformers.
4. **Sinusoidal absolute positional encodings** (`f29`) - Original transformer PE; natural precursor before queued RoPE (`08` / `f28`).
5. **NLL, CE, and log-softmax numerically stable form** (`f15`) - `logsumexp` trick pairs cleanly with the suggested softmax module; production numerics value.

_Queued but not yet shipped (not listed as gaps): Softmax Jacobian, LayerNorm, Focal Loss, CE vs KL, Adam/RMSProp, Weight Decay vs L2, RoPE, SwiGLU, KV-cache._

## Emerging

Filtered for intuition + derivation + small from-scratch PyTorch verify. Advanced variants whose base is not shipped are listed with `blocked_on` and were **not** merged into `topics.json`.

1. **Query-Key Normalization (QK-Norm)** - [Henry et al., Findings of EMNLP 2020](https://aclanthology.org/2020.findings-emnlp.379/) - \(\ell_2\)-normalize Q/K then learnable scale instead of fixed \(1/\sqrt{d_k}\). **Merged** (`qk_norm`). Prereq gate: attention scaling shipped.
2. **Logit soft-capping** - [Gemma 2 tech report, Google DeepMind](https://arxiv.org/abs/2408.00118) - \(\mathrm{soft\_cap}\cdot\tanh(\mathrm{logits}/\mathrm{soft\_cap})\). **Merged** (`logit_soft_capping`). Prereq gate: builds on scaled-softmax saturation; softmax is the intentional next foundation step.
3. **Normalization in Attention Dynamics** - [NeurIPS 2025](https://arxiv.org/abs/2510.22026) - ODE analysis of Pre/Post/Peri-LN token dynamics. `blocked_on: layernorm` (and Pre-LN vs Post-LN).
4. **nGPT (hypersphere-normalized Transformer)** - [ICLR 2025](https://openreview.net/forum?id=se4vjm7h4E) - unit-norm embeddings/weights/states. `blocked_on: layernorm`.
5. **AdaRoPE / learnable RoPE frequency variants** - recent RoPE extensions (head-wise frequencies / schedules). `blocked_on: rope`.

_Not merged (examples): ClockRoPE before RoPE; LoRA Intruder before LoRA; GQA before multi-head + KV-cache; Muon/SAM-style optimizers before Adam / weight-decay._

## Notes

- Papers With Code was not used.
- Manual statuses and titles in `topics.json` were preserved; at most two emerging items appended this run.
- X (`backlog/x_sources.md`) skipped silently after access block.
