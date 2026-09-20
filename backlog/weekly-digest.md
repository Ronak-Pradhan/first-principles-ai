# Weekly AI Math Digest

Generated: 2026-09-20 (2026-W38)

---

# Suggested Next Module

## Softmax Jacobian & Backpropagation (`softmax_jacobian`)

Overall Score: 39 / 40

Reason:

Module 01 (`attention_scaling`) remains the only shipped three-layer artifact. Softmax Jacobian is still the hinge that turns Attention Scaling into a trainable attention pathway: it derives `diag(p) - ppᵀ`, explains gradient flow through attention weights, and is a hard prerequisite for Multi-Head Attention and the FlashAttention path. LayerNorm and Adam match the raw score, and DDPM / LoRA remain close, but Softmax uniquely maximizes curriculum continuity from the only completed module. If the author builds only one module this week, this is the one that most improves the repository.

Prerequisites Satisfied

- ✅ Attention Scaling Factor (`attention_scaling`) - shipped under `modules/01_attention_scaling/` (`.md` + `.jpg` + `.ipynb`)

Unlocks

- Multi-Head Attention
- Causal / attention mask structure
- FlashAttention (with MHA + KV Cache + RoPE)
- Temperature scaling and sampling identities (with CE/softmax fluency)

Estimated Effort

| Task | Hours |
|------|------:|
| Research | 4 |
| Drawing | 3 |
| Implementation | 4 |
| Blog | 4 |
| Total | 15 |

---

# Repository Health

| Signal | State |
|--------|--------|
| Completed foundations | `attention_scaling` only (three-layer evidence present) |
| In-progress | Attention Scaling blog (`blog: wip`) |
| Queued foundations | Softmax → MHA → RoPE / KV Cache → FlashAttention; LayerNorm → SwiGLU; CE/KL → Focal / InfoNCE; Adam → Weight Decay; DDPM; LoRA |
| Domain coverage | Transformer Core is the only shipped domain; other domains exist as foundation queue plus emerging seeds (W31-W37 still absent from `main`, re-merged this week with W38 additions) |
| Curriculum continuity | Fragile: one shipped node; Softmax remains the missing hinge before the MHA spine |
| Prerequisite graph | Softmax blocks MHA, which blocks RoPE, KV Cache, GQA, and FlashAttention |
| Implementation backlog | 14 foundation topics still `github: todo`; emerging queue restored + expanded because prior weekly draft PRs never landed on `main` |
| Blog backlog | Attention Scaling blog WIP; all later topics unset |
| Research backlog | Attention Scaling research completed; all later topics unset |

Single largest curriculum weakness: Softmax Jacobian is still unbuilt, so the transformer spine cannot advance past Attention Scaling.

Underrepresented ML domains (shipped evidence): Vision, Representation Learning, Diffusion, RL, Recommendation, Audio, World Models, Graph ML, Quant Finance, Causal Inference, and Uncertainty Quantification all remain at zero shipped modules.

---

# Foundation Gaps

Evaluated every remaining foundation backlog topic with `scoring.md`. Softmax preferred over equal/near-equal scorers for continuity. Foundation curriculum was not modified.

| Rank | Topic | Score | Why Now | Unlocks |
|------|------:|--------|----------|----------|
| 1 | Softmax Jacobian (`softmax_jacobian` / f02) | 39 | Only completed prereq is shipped; interview- and systems-critical Jacobian | MHA, masks, FlashAttention path |
| 2 | Layer Normalization (`layernorm` / f03) | 39 | No backlog prereqs; stabilizer for every transformer block | RMSNorm, Pre/Post-LN, SwiGLU, Peri-LN family |
| 3 | Adam from First Principles (`adam_optimizer` / f12) | 39 | No backlog prereqs; unlocks adaptive optimization lineage | Weight decay vs L2, AdaGrad/RMSProp variants, modern optimizers |
| 4 | LoRA (`lora` / f08) | 38 | Portfolio magnet; independent of Softmax path | QLoRA and other low-rank adapters (after LoRA) |
| 5 | Cross Entropy vs KL (`cross_entropy_vs_kl` / f10) | 38 | Information-theory bridge with no backlog prereqs | Focal Loss, InfoNCE, label smoothing, distillation |

Also scored highly but deferred for continuity or prerequisites: DDPM forward process (38), Multi-Head Attention (38 objective, blocked on Softmax for sequencing), Residual connections (39 objective, present in `foundation_curriculum.json` but absent from `topics.json` - see Missing Links).

---

# Missing Links

Highest-impact conceptual holes relative to the current graph:

1. Residual connections as identity gradient highways (`f07`) - required before Pre-LN vs Post-LN and modern residual variants; in foundation curriculum but absent from `topics.json`.
2. Causal / attention mask structure (`f08`) - additive `-inf` mask before Softmax; natural companion once Softmax Jacobian ships.
3. Softmax Jacobian itself - the live hinge between Attention Scaling and Multi-Head Attention.
4. ELBO + reparameterization trick before deep DDPM reverse-process / VAE work - already seeded as emerging (`elbo_variational_bound`, `reparameterization_trick`).
5. Score matching beside DDPM / flow matching - closes the generative modeling triangle; seeded as `score_matching`.
6. Log-derivative trick + Bellman expectation + TD / Advantage before REINFORCE-style objectives - seeded as `log_derivative_trick`, `bellman_expectation`, `temporal_difference_learning`, `advantage_function`, and `gae_generalized_advantage`.
7. Itô's Lemma before a first-principles Black-Scholes derivation - seeded this week as `ito_lemma` (Black-Scholes PDE already queued as `black_scholes_pde`).
8. Short-time Fourier transform before Mel filterbank - `short_time_fourier_transform` precedes `mel_filterbank` in the emerging graph.
9. Wasserstein distance before relying solely on Sinkhorn iterations - seeded this week as `wasserstein_distance`.

---

# Emerging Candidates

Accepted only if score ≥ 30, portfolio fit gates pass, and prerequisites are satisfiable from current/queued topics (not advanced variants of unbuilt modules).

## Revalidated (still absent from `main`; re-merged)

| Topic | Domain | Score | Confidence | Why Interesting | Blocked On |
|--------|--------|------:|------------|-----------------|------------|
| `qk_norm` | Modern Transformers | 34 | High | Per-vector Q/K normalization stabilizing attention logits | attention_scaling (satisfied) |
| `elbo_variational_bound` | Generative Models | 37 | High | Core latent-variable identity; unlocks VAEs and disciplined DDPM reading | - |
| `flow_matching` | Diffusion | 36 | High | Simulation-free vector-field regression; evergreen alternative to score SDEs | - |
| `score_matching` | Diffusion | 36 | High | Denoising score matching links noise prediction to ∇ log p | - |
| `gumbel_softmax` | Discrete Latents | 35 | High | Reparameterization for categorical latents | - |
| `message_passing` | Graph ML | 36 | High | GNN backbone aggregation math | - |
| `ctc_loss` | Sequence Losses | 34 | High | Alignment-free sequence loss via DP | - |
| `two_tower_retrieval` | Recommendation | 34 | High | Dual-encoder similarity learning | - |
| `vit_patch_embedding` | Computer Vision | 35 | High | Patchify + linear projection tokenization | - |
| `inverse_propensity_weighting` | Causal Inference | 33 | High | Reweighting identity for observational bias | - |
| `jepa_predictive_objective` | World Models | 33 | Medium | Predict-in-embedding space without pixels | - |
| `black_scholes_pde` | Quantitative Finance | 34 | High | Option PDE from hedge argument | - |
| `sinkhorn_optimal_transport` | Optimal Transport | 32 | Medium | Entropic OT row/column scaling | - |
| `bpr_ranking_loss` | Recommendation | 33 | High | Pairwise logistic ranking for implicit feedback | - |
| `kalman_filter` | State Estimation | 34 | High | Gaussian predict-update recursion | - |
| `short_time_fourier_transform` | Audio / Speech | 33 | High | Windowed DFT front door to spectrograms | - |
| `mel_filterbank` | Audio / Speech | 32 | High | Mel-scale triangular filters over STFT | short_time_fourier_transform (queued) |
| `vicreg` | Representation Learning | 30 | Medium | Variance / invariance / covariance anti-collapse | - |
| `log_derivative_trick` | Reinforcement Learning | 36 | High | ∇ log π identity; REINFORCE gateway | - |
| `importance_sampling` | Monte Carlo Inference | 34 | High | Change-of-measure estimator | - |
| `gaussian_mixture_em` | Foundations | 34 | High | EM responsibilities + closed-form M-step | - |
| `barlow_twins` | Representation Learning | 31 | Medium | Cross-correlation redundancy reduction | - |
| `reparameterization_trick` | Generative Models | 39 | High | Pathwise Gaussian reparameterization for ELBO grads | - |
| `bellman_expectation` | Reinforcement Learning | 36 | High | V = R + γPV recursive identity | - |
| `natural_gradient` | Optimization | 34 | High | Fisher-preconditioned update | - |
| `hutchinson_trace_estimator` | Numerical Linear Algebra | 32 | Medium | Stochastic trace probes | - |
| `spectral_normalization` | Computer Vision | 31 | Medium | Power-iteration Lipschitz control | - |
| `byol_bootstrap` | Representation Learning | 30 | Medium | EMA target bootstrap without negatives | - |

## New this week (merged)

| Topic | Domain | Score | Confidence | Why Interesting | Blocked On |
|--------|--------|------:|------------|-----------------|------------|
| `conformal_prediction` | Uncertainty Quantification | 36 | High | Exchangeability + calibration quantile → finite-sample coverage; new underrepresented domain | - |
| `ito_lemma` | Quantitative Finance | 34 | High | Itô calculus bridge into Black-Scholes and continuous diffusion SDEs | - |
| `temporal_difference_learning` | Reinforcement Learning | 38 | High | TD(0) bootstrap δ = r + γV(s′) − V(s); unlocks practical RL after Bellman | bellman_expectation (queued) |
| `advantage_function` | Reinforcement Learning | 37 | High | A = Q − V baseline identity for actor-critic / policy gradients | bellman_expectation (queued) |
| `wasserstein_distance` | Optimal Transport | 33 | High | Earth-mover / Kantorovich geometry before Sinkhorn specialization | - |
| `backdoor_adjustment` | Causal Inference | 33 | High | do-calculus identification via blocking backdoor paths; pairs with IPW | - |
| `fourier_feature_mapping` | Computer Vision | 32 | High | Random Fourier features for high-frequency coordinate networks | - |
| `gae_generalized_advantage` | Reinforcement Learning | 36 | High | λ-weighted TD residual advantages; bias-variance dial used across modern policy gradients | temporal_difference_learning + advantage_function (queued) |

---

# Blocked Candidates

Topics worth revisiting after prerequisite modules are complete. Scored where useful, but **not** merged into `topics.json`.

| Topic | Waiting For | Notes |
|--------|-------------|-------|
| Peri-LN / HybridNorm / Mix-LN / DeepNorm residual scaling | LayerNorm + Residual connections | NeurIPS 2025 normalization-dynamics and HybridNorm are real mechanisms, but they are placement variants of unbuilt foundations |
| Sigmoid attention (incl. Flash-Sigmoid kernels) | Softmax Jacobian (+ preferably MHA) | Softmax alternative; teach Softmax path first |
| Hierarchical / multi-scale self-attention | Multi-Head Attention | Nested-signal generalization of Softmax attention |
| Multi-Token Attention / differential / gated attention | Multi-Head Attention | Architectural attention variants |
| GQA / MQA | Multi-Head Attention + KV Cache | Foundation `f32`; advanced memory tradeoff |
| FlashAttention v2 / v3 | FlashAttention (`f33`) | IO-aware tiling refinements |
| YaRN / ClockRoPE / other RoPE extrapolations | RoPE | Position-encoding variants |
| QLoRA / LoRA+ family | LoRA | Adapter variants |
| Muon / Newton-Schulz orthogonalized optimizers | Adam | Optimizer variants before Adam ships |
| MoE router variants (KERN, load-balance tricks) | MoE routing foundation (`f34`) | Routing refinements |
| Consistency models / sCM / rectified-flow / OT-CFM | DDPM (+ preferably flow matching) | Generative shortcuts before forward-process foundation |
| AIPW / Neyman orthogonal score | Inverse Propensity Weighting (`inverse_propensity_weighting`) | Doubly robust upgrade path |
| GAT / Graph Attention | Message Passing (`message_passing`) (+ MHA) | Attention-on-graphs before neighborhood aggregation |
| Particle filter / RTS Kalman smoother | Kalman Filter (`kalman_filter`) | Nonlinear / smoothing extensions |
| Black-Scholes Greeks | Black-Scholes PDE + Itô (`black_scholes_pde`, `ito_lemma`) | Sensitivity layer after PDE |
| Speculative decoding (as emerging) | Foundation `f35` + sampling / KV Cache | Keep on foundation track |
| Causal-JEPA / SIGReg | JEPA predictive objective (`jepa_predictive_objective`) | Causal world-model variants |
| Sparse / linear / compressed attention kernels | MHA (+ systems path) | Efficiency variants |

---

# Rejected This Week

| Topic | Reason |
|--------|--------|
| Diffusion-Adaptive Routing / Mixture-of-States / SharpMoE routing | Paper-specific DiT/MoE system stacks; not a reusable first-principles mechanism |
| KRPO / KTAE token-advantage estimators | Composite RLHF training tricks; depend on GRPO-style stacks rather than a clean math object |
| MAD-TD / high-UTD model-augmented TD | Algorithmic system recipe; TD(0) itself is the evergreen mechanism (merged as `temporal_difference_learning`) |
| Sparsemax / Soft-DTW | Score < 30 for portfolio + implementation clarity relative to Softmax / CTC |
| Straight-Through Estimator alone | Thin as a standalone module; better as a note inside discrete-latent modules |
| Neural ODE adjoint sensitivity | Implementation-heavy; weak handwritten-visual payoff for this repo's format |
| InfoNCE aliases / NT-Xent renames | Duplicate of foundation `info_nce` |
| Product model launches, benchmarks, hardware kernels, prompt tips | Fail authenticity / portfolio gates in `scoring.md` |
| Formal-math / product posts from OpenAI & Anthropic surfaces | No reusable ML mechanism extracted this week |
| Scaling-laws-only writeups | Descriptive empirics without a derivable mechanism |

---

# Repository Coverage

| Area | Coverage |
|------|----------|
| Transformer Core | Shipped: Attention Scaling. Queued: Softmax, LN, MHA, RoPE, KV, Flash, SwiGLU. Emerging: `qk_norm` |
| Optimization | Foundation: Adam, weight decay. Emerging: `natural_gradient` |
| Loss Functions | Foundation: CE/KL, Focal, InfoNCE. Emerging: `ctc_loss`, `bpr_ranking_loss` |
| Diffusion / Generative | Foundation: DDPM. Emerging: `elbo_variational_bound`, `reparameterization_trick`, `score_matching`, `flow_matching`, `sinkhorn_optimal_transport`, `wasserstein_distance` |
| Reinforcement Learning | Foundation: REINFORCE / KL-RL sketches. Emerging: `log_derivative_trick`, `bellman_expectation`, `temporal_difference_learning`, `advantage_function`, `gae_generalized_advantage`, `importance_sampling` |
| Computer Vision | Emerging: `vit_patch_embedding`, `spectral_normalization`, `fourier_feature_mapping` |
| Representation Learning | Emerging: `vicreg`, `barlow_twins`, `byol_bootstrap` |
| Recommendation Systems | Emerging: `two_tower_retrieval`, `bpr_ranking_loss` |
| World Models | Emerging: `jepa_predictive_objective` |
| Audio / Speech | Emerging: `short_time_fourier_transform` → `mel_filterbank`, `ctc_loss` |
| Graph ML | Emerging: `message_passing` |
| Quantitative Finance | Emerging: `ito_lemma`, `black_scholes_pde` |
| Causal Inference | Emerging: `inverse_propensity_weighting`, `backdoor_adjustment` |
| Uncertainty Quantification | Emerging: `conformal_prediction` (new) |
| State Estimation | Emerging: `kalman_filter` |

---

# Notes

- Suggested next module is unchanged for the right reason: Softmax Jacobian is still unquestionably the highest-leverage build while only Attention Scaling is shipped.
- W31-W37 emerging merges still had not landed on `main` as of this run; all previously accepted emerging topics were revalidated against `scoring.md` and re-merged.
- New W38 merges prioritize missing mathematical bridges (Itô, Wasserstein, TD/Advantage/GAE) and underrepresented domains (conformal prediction, backdoor adjustment, Fourier features) rather than Transformer novelty.
- Foundation curriculum and manual topic statuses were not modified.
- Domains explored: Transformers, Vision, Representation Learning, Diffusion / OT, Reinforcement Learning, Recommendation, Audio, World Models, Graph ML, Quantitative Finance, Causal Inference, Uncertainty Quantification, Optimization / information geometry.
- Sources unavailable: X/Twitter (Tier 5) not queried. OpenAI / Anthropic research surfaces reachable but mostly product / formal-math posts rather than reusable ML mechanisms.
