# Weekly AI Math Digest (2026-W31)

_Generated 2026-07-30. Sources: `foundation_curriculum.json` gap rank; arXiv cs.LG; Hugging Face blog RSS; Anthropic / DeepMind / Meta / Microsoft Research / OpenAI pages (best-effort). X lookups unreachable this run._

## Suggested next module

**Softmax Jacobian and backpropagation** (`softmax_jacobian`, curriculum `f02`).

Module `01_attention_scaling` is the only shipped three-layer module (brief + canvas + notebook). Softmax is the immediate operator after the scaled logits that module justifies, and the full Jacobian \(\operatorname{diag}(p)-pp^\top\) is both interview-critical and the right depth for a derivation-plus-empirical portfolio piece. It is already queued in `topics.json` with no module path yet, so shipping it extends the transformer-core spine without jumping ahead of prerequisites.

## Foundation gaps

Ranked uncovered classics (curriculum vs backlog/modules; only `attention_scaling` has three-layer evidence):

1. **Softmax Jacobian and backpropagation** (`f02`) - Natural follow-on from shipped attention scaling; interview staple; deep matrix calculus.
2. **LayerNorm forward and backward** (`f03`) - Default transformer stabilizer; subtle backward pass; high longevity across every modern stack.
3. **Multi-head attention as partitioned subspaces** (`f09`) - Direct architectural sequel to scaled dot-product; clarifies \(d_k=d_{\mathrm{model}}/h\) compute tradeoffs.
4. **RoPE multi-dimensional derivation** (`f28`) - Industry-default positional math; strong portfolio value after attention logits are solid.
5. **Causal / attention mask structure** (`f08`) - Completes decoder attention legality (additive \(-\infty\) before softmax); short but foundational.

## Emerging

Filtered for math/architecture concepts suitable for a deep derivation module (dropped datasets, benchmarks, hardware-only, and training tricks without new math). X skipped (unreachable).

- [Self-Attention Dynamics with Rotary Position Embeddings](https://arxiv.org/abs/2607.24502) - Continuous-time spherical attention dynamics under RoPE rotations; derivation-ready positional math.
- [ClockRoPE: Random Fourier Rotations for Temporal Routine Modeling](https://arxiv.org/abs/2607.26369) - Revisits RoPE frequency schedules beyond log-linear decay; clean follow-on to foundation RoPE.
- [The Intruder Threshold: A Spectral Law for LoRA Fine-Tuning](https://arxiv.org/abs/2607.23711) - Per-layer spectral condition for LoRA “intruder” singular vectors; SVD-level fine-tuning theory.
- [Sharpness-Aware Minimization and Muon: Robustness under the Spectral Norm](https://arxiv.org/abs/2607.26001) - Optimizer geometry under spectral-norm perturbations; bridges SAM and Muon.
- [A Compositional Theory of Causally Masked Transformers](https://arxiv.org/abs/2607.26988) - Algebraic/finite-precision account of what causal transformers can compute.
- [Flow Map Learning via Nongradient Vector Flow](https://arxiv.org/abs/2607.26398) - Consistency-style flow maps without gradient vector fields; generative-model math.
- [Scale Weight Decay and Train Better](https://arxiv.org/abs/2607.23777) - Robbins–Monro-inspired scaling of decoupled weight decay under data scaling.
- [A Coulomb Particle Model for Learning Kernel Attention](https://arxiv.org/abs/2607.23869) - Riesz/Coulomb-regularized particles for kernel attention feature distributions.
- [DiffusionGemma (text diffusion)](https://blog.google/innovation-and-ai/technology/developers-tools/diffusion-gemma-faster-text-generation/) - Lab open model using block text diffusion instead of token AR; discrete diffusion architecture concept.
