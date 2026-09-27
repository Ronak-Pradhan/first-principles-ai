# Weekly AI Math Digest

Generated: 2026-09-27 (2026-W39)

---

# Suggested Next Module

## Softmax Jacobian & Backpropagation (`softmax_jacobian`)

Overall Score: **39 / 40**

Reason:

Only `attention_scaling` has three-layer evidence. Softmax is the live hinge on that spine: its Jacobian `diag(p) - ppᵀ` explains saturation, gradient flow, and every downstream attention / sampling / contrastive module. LayerNorm and Adam can match the raw score, but Softmax uniquely continues the single completed module and unlocks Multi-Head Attention. If the author builds only one module this week, this is the one.

Prerequisites Satisfied

- ✅ Attention Scaling Factor (`attention_scaling`) - shipped under `modules/01_attention_scaling/`
- ✅ Softmax as an operator already appears in the attention-scaling derivation

Unlocks

- Multi-Head Attention
- Causal / attention masks
- FlashAttention path (with MHA + KV + RoPE)
- Temperature scaling, top-k / top-p sampling
- Cross-entropy / KL and InfoNCE numerical stories

Estimated Effort

| Task | Hours |
|------|------:|
| Research | 4 |
| Drawing | 3 |
| Implementation | 4 |
| Blog | 3 |
| Total | 14 |

---

# Repository Health

| Signal | State |
|--------|--------|
| Completed foundations | `attention_scaling` only (`.md` + `.jpg` + `.ipynb` present) |
| Queued foundations | Softmax, LayerNorm, MHA, RoPE, KV Cache, FlashAttention (intentional), LoRA, SwiGLU, CE vs KL, Focal Loss, Adam, Weight Decay vs L2, InfoNCE, DDPM |
| Domain coverage | Transformer Core is the only shipped domain; other domains exist only as backlog / emerging seeds |
| Curriculum continuity | Broken after module 01 - Softmax missing before MHA |
| Prerequisite graph | Attention → Softmax → MHA → {RoPE, KV, Flash}; LayerNorm → SwiGLU / Pre-LN; Adam → weight decay; CE/KL → Focal / InfoNCE |
| Implementation backlog | Softmax + LayerNorm + Residuals + MHA dominate |
| Blog backlog | Attention Scaling blog still `wip`; all other blogs `todo` |
| Research backlog | Softmax research not started |

**Largest curriculum weakness:** Softmax Jacobian absence stalls the entire transformer spine.

**Underrepresented ML domains (shipped evidence):** Vision, Representation Learning, Diffusion, RL, RecSys, Audio, World Models, Graph ML, Quant Finance, Causal Inference - all empty in `modules/`.

---

# Foundation Gaps

Evaluated remaining foundation curriculum topics with `scoring.md`. Scores are objective; order below is recommendation priority after the Softmax continuity preference.

| Rank | Topic | Score | Why Now | Unlocks |
|------|------:|--------|----------|----------|
| 1 | Softmax Jacobian (`f02` / `softmax_jacobian`) | 39 | Continuity from shipped attention scaling; interview + systems critical | MHA, masks, FlashAttention, sampling, CE path |
| 2 | LayerNorm forward/backward (`f03` / `layernorm`) | 39 | Parallel stabilizer; no Softmax dependency | RMSNorm, Pre/Post-LN, SwiGLU block |
| 3 | Adam first/second moment (`f17` / `adam_optimizer`) | 39 | Evergreen optimizer; no transformer prereq | Weight decay vs L2, schedules, μP |
| 4 | Residual identity highways (`f07`) | 38 | Missing bridge in foundation curriculum not yet in `topics.json` | Pre/Post-LN, deep nets, HybridNorm later |
| 5 | Multi-Head Attention (`f09` / `multi_head_attention`) | 38 | Spine unlock - blocked until Softmax ships | RoPE, KV Cache, GQA, FlashAttention |
| - | LoRA (`f46`) | 38 | Strong portfolio; independent prereqs | QLoRA later |
| - | Cross Entropy vs KL (`f11`) | 38 | Loss spine | Focal, label smoothing, InfoNCE |
| - | DDPM forward (`f48`) | 37 | Highest non-transformer portfolio unlock | Score/flow, guidance, consistency later |
| - | Causal / attention mask (`f08`) | 36 | Needs Softmax + attention scaling | Autoregressive legality, ALiBi |
| - | InfoNCE (`f16`) | 36 | Needs CE/KL | CLIP, retrieval, VICReg neighbors |

Foundation preferred over emerging unless an emerging topic clearly outranks. None did this week.

---

# Missing Links

Highest-impact conceptual holes (often higher priority than new research):

1. **Softmax Jacobian** - live hinge after Attention Scaling
2. **Residual connections (`f07`)** - in foundation curriculum, absent from `topics.json`
3. **Causal / attention mask (`f08`)** - needed before ALiBi and legal decoding stories
4. **ELBO + reparameterization** before deep DDPM / VAE work (emerging seeds present; not shipped)
5. **Score matching + Langevin** beside DDPM / flow matching
6. **Log-derivative + Bellman + TD / Advantage** before REINFORCE / PPO / GRPO depth
7. **Itô's Lemma** before first-principles Black-Scholes depth
8. **STFT** before Mel filterbank
9. **Wasserstein distance** before Sinkhorn-only optimal transport
10. **Graph Laplacian** beside message passing (spectral bridge)

---

# Emerging Candidates

Accepted this week (pass `scoring.md`, prereq gate, portfolio fit). Confidence reflects mechanism clarity and implementation friendliness.

| Topic | Domain | Score | Confidence | Why Interesting | Blocked On |
|--------|--------|------:|------------|-----------------|------------|
| Group-Relative Advantage Whitening | RL | 36 | High | Critic-free Â=(r-μ)/σ group baseline behind GRPO | Advantage Function (queued emerging) |
| PPO Clipped Surrogate | RL | 34 | High | min(ρÂ, clip(ρ,1-ε,1+ε)Â) trust-region identity | Advantage + log-derivative |
| Langevin Dynamics Sampling | Monte Carlo / Diffusion | 35 | High | Score-driven SDE; bridge MCMC ↔ score-based generation | Score matching (queued emerging) |
| Metropolis-Hastings | Monte Carlo | 33 | High | Detailed-balance accept-reject; MALA correction | None |
| Control Variates | Monte Carlo | 33 | High | X-β(Y-E[Y]) variance reduction; REINFORCE baseline math | None |
| Graph Laplacian Spectral Smoothing | Graph ML | 33 | High | L=D-A smoothness quadratic; spectral GNN root | None |
| Polyak Averaging (EMA) | Optimization | 32 | High | θ̄←τθ̄+(1-τ)θ; BYOL / SWA / diffusion teachers | None |
| Front-Door Adjustment | Causal | 32 | Medium | Mediator identification when back-door fails | Back-door adjustment |
| Maximum Mean Discrepancy | Representation | 31 | Medium | Kernel two-sample ||μ_P-μ_Q||_H | None |
| FiLM Conditioning | Vision / Multimodal | 31 | Medium | γ(z)⊙x+β(z) feature-wise affine conditioning | None |
| Sparse Dictionary Learning | Representation | 31 | Medium | Sparse coding objective behind SAE feature decomposition | None |

Revalidated prior emerging set (still absent from `main`, still pass gates): `qk_norm` through `gae_generalized_advantage` (W31-W38).

---

# Blocked Candidates

Worth revisiting after prerequisites. Listed in digest only - **not** merged.

| Topic | Waiting For |
|--------|-------------|
| SpanNorm / SiameseNorm / Peri-LN / HybridNorm / DeepNorm | LayerNorm + Residual connections |
| STAR MoE routing / Attention-Aware Routing / other MoE routers | Mixture-of-Experts foundation (`f34`) |
| Norm×Direction linear attention (NaLaFormer) | Softmax + Multi-Head Attention |
| MonarchAttention / CEDAR / Routed-Memory / MARCH / Declarative Attention | MHA + KV Cache (+ FlashAttention path for some) |
| FlashAttention v2 / v3 | FlashAttention (`f33`) |
| GQA / MQA | Multi-Head Attention + KV Cache |
| YaRN / RoPE variants | RoPE |
| QLoRA / LoRA variants | LoRA |
| Muon / Newton-Schulz orthogonalized updates | Adam |
| Consistency models / sCM / rectified-flow / OT-CFM / Contrastive Flow Matching | DDPM and/or Flow Matching shipped |
| Probability-flow ODE / DDIM / Classifier-free guidance | DDPM |
| AIPW / Neyman orthogonal score | Inverse Propensity Weighting |
| GAT / causal message-passing composites | Message Passing |
| Particle filter / RTS smoother | Kalman Filter |
| Black-Scholes Greeks | Black-Scholes PDE + Itô |
| Speculative decoding (as emerging) | Foundation `f35` (already curated) |
| SIGReg / Causal-JEPA | JEPA predictive objective shipped |
| Multi-token / sigmoid / hierarchical / gated / differential attention | Softmax + Multi-Head Attention |
| Sparse / compressed / Infini-attention | MHA + KV Cache |

---

# Rejected This Week

| Topic | Reason |
|--------|--------|
| Sparsemax | Score 28 (<30); also premature before Softmax ships |
| Soft-DTW | Score 26 (<30); niche sequence alignment |
| Model / lab product posts (Anthropic Claude tools, OpenAI sparse-transformer marketing) | Not reusable first-principles mechanisms |
| FlashPairformer / hardware kernels | Engineering acceleration, not evergreen math module |
| 1-shot RLVR / SPARKLE / Atomic Thinking benchmarks | Evaluation frameworks and training recipes, not mechanisms |
| DeepSeek / DiT / MoE system stacks | Composite product architectures |
| InfoNCE aliases / CPC renames | Novelty gate - foundation `f16` already covers |
| Straight-Through Estimator alone | Score <30 without Gumbel-Softmax framing |
| Neural ODE adjoint | Excessive implementation / drawing cost for one module |
| Prompt engineering / Declarative Attention protocols | Not mathematical mechanisms |
| Scaling-laws-only writeups | Empirical curves without implementable identity |
| Benchmarks, datasets, API launches | Hard reject per `sources.md` |

---

# Repository Coverage

| Area | Coverage |
|------|----------|
| Transformer Core | Shipped: Attention Scaling. Queued: Softmax, LN, MHA, RoPE, KV, Flash, SwiGLU. Emerging: QK-Norm |
| Optimization | Queued: Adam, Weight Decay. Emerging: Natural Gradient, Polyak Averaging |
| Loss Functions | Queued: CE vs KL, Focal, InfoNCE. Emerging: CTC, BPR |
| Diffusion | Queued: DDPM. Emerging: ELBO, reparameterization, score matching, flow matching, Langevin |
| Reinforcement Learning | Queued: REINFORCE / KL-RL in foundation curriculum. Emerging: log-derivative, Bellman, TD, Advantage, GAE, group-relative advantage, PPO clip |
| Computer Vision | Emerging: ViT patch embedding, spectral norm, Fourier features, FiLM |
| Representation Learning | Queued: InfoNCE. Emerging: VICReg, Barlow, BYOL, JEPA, MMD, sparse dictionary learning |
| Recommendation Systems | Emerging: Two-tower retrieval, BPR |
| World Models | Emerging: JEPA predictive objective |
| Audio / Speech | Emerging: STFT → Mel, CTC |
| Graph ML | Emerging: Message passing, Graph Laplacian |
| Quantitative Finance | Emerging: Black-Scholes PDE, Itô |
| Causal Inference | Emerging: IPW, back-door, front-door |
| Monte Carlo / Uncertainty | Emerging: Importance sampling, Metropolis-Hastings, control variates, conformal prediction, Hutchinson trace |
| Optimal Transport | Emerging: Sinkhorn, Wasserstein |

---

# Notes

- Suggested next module remains **Softmax Jacobian**. No emerging topic outranks unfinished transformer-core foundations on curriculum continuity.
- New topics merged into `topics.json` (W39): `group_relative_advantage`, `langevin_dynamics`, `metropolis_hastings`, `control_variates`, `polyak_averaging`, `front_door_adjustment`, `graph_laplacian`, `film_conditioning`, `ppo_clipped_surrogate`, `maximum_mean_discrepancy`, `sparse_dictionary_learning`.
- Re-merged (still absent from `main`, revalidated): full W31-W38 emerging set (`qk_norm` through `gae_generalized_advantage`), with Mel still requiring STFT and GAE requiring TD+Advantage.
- Existing manual topics / statuses / titles / `interest_domains` / `foundation_curriculum.json` were not modified.
- Prior weekly digest PRs (#7-#11) remain unmerged drafts; this run re-validates against current `main`.
- Sources unavailable: X/Twitter (Tier 5) unused by policy (optional). OpenAI / Anthropic research surfaces were mostly interpretability or product posts; extracted only the sparse dictionary-learning mechanism where it passed scoring.
