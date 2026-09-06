# Weekly AI Math Digest

Generated: 2026-09-06 (2026-W36)

---

# Suggested Next Module

## Softmax Jacobian & Backpropagation (`softmax_jacobian`)

Overall Score: 39 / 40

Reason:

Module 01 (`attention_scaling`) is the only shipped three-layer artifact. Softmax Jacobian is the immediate foundation bridge on that path: it derives `diag(p) - ppᵀ`, explains gradient flow through attention weights, and is a hard prerequisite for Multi-Head Attention and FlashAttention. Adam and LayerNorm can match the raw score, but Softmax uniquely maximizes curriculum continuity from the only completed module. If the author builds only one module this week, this is the one that most improves the repository.

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
| Domain coverage | Almost entirely Transformer Core on the critical path; other domains exist only as queued foundations or newly merged emerging seeds |
| Curriculum continuity | Fragile: one shipped node; Softmax is the missing hinge before the MHA spine |
| Prerequisite graph | Softmax blocks MHA, which blocks RoPE, KV Cache, GQA, and FlashAttention |
| Implementation backlog | 14 foundation topics still `github: todo`; emerging queue newly restored after prior draft PRs never landed on main |
| Blog backlog | Attention Scaling blog WIP; all later topics unset |
| Research backlog | Attention Scaling research completed; all later topics unset |

Single largest curriculum weakness: Softmax Jacobian is still unbuilt, so the transformer spine cannot advance past Attention Scaling.

---

# Foundation Gaps

Evaluated remaining foundation topics with `scoring.md`. Softmax preferred over equal/near-equal scorers for continuity.

| Rank | Topic | Score | Why Now | Unlocks |
|------|------:|--------|----------|----------|
| 1 | Softmax Jacobian (`softmax_jacobian` / f02) | 39 | Only completed prereq is shipped; interview- and systems-critical Jacobian | MHA, masks, FlashAttention path |
| 2 | Layer Normalization (`layernorm` / f03) | 39 | No backlog prereqs; stabilizer for every transformer block | RMSNorm, Pre/Post-LN, SwiGLU, Peri-LN family |
| 3 | Adam from First Principles (`adam_optimizer` / f12) | 39 | No backlog prereqs; unlocks adaptive optimization lineage | Weight decay vs L2, AdaGrad/RMSProp variants, modern optimizers |
| 4 | LoRA (`lora` / f08) | 38 | Portfolio magnet; independent of Softmax path | QLoRA and other low-rank adapters (after LoRA) |
| 5 | Cross Entropy vs KL (`cross_entropy_vs_kl` / f10) | 38 | Information-theory bridge with no backlog prereqs | Focal Loss, InfoNCE, label smoothing, distillation |

Also scored highly but deferred for continuity or prerequisites: DDPM forward process (38), Multi-Head Attention (38, blocked on Softmax), Residual connections (39 objective, not yet in `topics.json` - see Missing Links).

---

# Missing Links

Highest-impact conceptual holes relative to the current graph:

1. Residual connections as identity gradient highways (`f07`) - required before Pre-LN vs Post-LN and modern residual variants; absent from `topics.json`.
2. Causal / attention mask structure (`f08`) - additive `-inf` mask before Softmax; natural companion once Softmax Jacobian ships.
3. Softmax Jacobian itself - the live hinge between Attention Scaling and Multi-Head Attention.
4. ELBO variational bound - should precede deep DDPM reverse-process work; merged this week as emerging seed `elbo_variational_bound`.
5. Score matching beside DDPM / flow matching - closes the generative modeling triangle; merged as `score_matching`.
6. Log-derivative trick - missing RL bridge before REINFORCE / RLHF-style objectives; merged as `log_derivative_trick`.

---

# Emerging Candidates

Accepted only if score ≥ 30, portfolio fit gates pass, and prerequisites are satisfiable from current/queued foundations (not advanced variants of unbuilt modules).

| Topic | Domain | Score | Confidence | Why Interesting | Blocked On |
|--------|--------|------:|------------|-----------------|------------|
| elbo_variational_bound | Diffusion / Generative | 37 | High | Core latent-variable identity; unlocks VAEs and disciplined DDPM reading | - |
| flow_matching | Diffusion / Generative | 36 | High | Simulation-free vector-field regression; evergreen alternative to score SDEs | - |
| score_matching | Diffusion / Generative | 36 | High | Denoising score matching links noise prediction to ∇ log p | - |
| gumbel_softmax | Representation / Discrete | 35 | High | Reparameterization for categorical latents; widely reused | - |
| message_passing | Graph ML | 35 | High | GNN backbone aggregation math | - |
| log_derivative_trick | Reinforcement Learning | 35 | High | ∇ log π identity; foundation for REINFORCE / policy gradients | - |
| importance_sampling | Foundations / Inference | 34 | High | Change-of-measure estimator; appears across RL, eval, and Monte Carlo | - |
| qk_norm | Transformers | 34 | High | Per-vector Q/K normalization stabilizing attention logits | attention_scaling (satisfied) |
| jepa_predictive_objective | World Models | 34 | Medium | Predict-in-embedding space without pixel reconstruction | - |
| ctc_loss | Audio / Speech | 34 | High | Alignment-free sequence loss via dynamic programming | - |
| black_scholes_pde | Quantitative Finance | 34 | High | Closed-form PDE derivation with hedge argument | - |
| inverse_propensity_weighting | Causal Inference | 33 | High | Reweighting identity for observational bias | - |
| bpr_ranking_loss | Recommendation | 33 | High | Pairwise logistic ranking from implicit feedback | - |
| two_tower_retrieval | Recommendation / Embeddings | 33 | High | Dual-encoder similarity learning mechanism | - |
| kalman_filter | World Models / Signal | 33 | High | Predict-update Gaussian filtering; transferable state estimation | - |
| gaussian_mixture_em | Foundations | 33 | High | EM as alternating E-step responsibilities and M-step MLE | - |
| sinkhorn_optimal_transport | Diffusion / OT | 32 | Medium | Entropic OT iterations; couples to flow / transport paths | - |
| vit_patch_embedding | Vision | 32 | High | Patchify + linear projection as vision tokenization | - |
| mel_filterbank | Audio / Speech | 32 | High | Mel-scale triangular filter math under STFT features | - |
| barlow_twins | Representation Learning | 31 | Medium | Cross-correlation redundancy reduction; distinct from VICReg | - |
| vicreg | Representation Learning | 30 | Medium | Variance-invariance-covariance collapse prevention | - |

---

# Blocked Candidates

Topics worth revisiting after prerequisite modules are complete. Not merged into `topics.json`.

| Topic | Waiting For |
|--------|-------------|
| Grouped Query / Multi-Query Attention | Multi-Head Attention + KV Cache |
| FlashAttention v2 / IO kernel variants | FlashAttention |
| YaRN / Long-RoPE variants | RoPE |
| QLoRA / LoRA+ / DoRA | LoRA |
| Muon / Newton-Schulz orthogonalized updates | Adam |
| Peri-LN / HybridNorm / DeepNorm placement variants | LayerNorm + Residual connections |
| KERN / Nadaraya-Watson MoE routers | Mixture-of-Experts routing foundation |
| Compressed / Heavily Compressed / DeepSeek Sparse Attention | Multi-Head Attention + KV Cache |
| Manifold-Constrained Hyper-Connections (mHC) | Residual connections |
| SIGReg / LeJEPA regularizer | JEPA predictive objective |
| Black-Scholes Greeks taxonomy | Black-Scholes PDE |
| AIPW / doubly robust estimators | Inverse propensity weighting |
| Neyman orthogonal score | Inverse propensity weighting |
| Rectified flow / OT-CFM variants | Flow Matching |
| Speculative decoding acceptance math | Already foundation `f35`; needs sampling + KV Cache |
| Gated / differential / multi-token attention variants | Multi-Head Attention |

---

# Rejected This Week

| Topic | Reason |
|--------|--------|
| DeepSeek-V4 / CSA+HCA product stack | Model release + composite architecture; not a single reusable mechanism |
| EAGLE 3.1 speculative decoding fix | Engineering variant of speculative decoding; prerequisite and novelty gates fail |
| OpenAI / Anthropic formal-math product posts | Not an ML mathematical mechanism for this curriculum |
| Process supervision as standalone module | Alignment training recipe without a clean first-principles mechanism beyond reward modeling |
| VarCon (variational supervised contrastive) | Paper-specific objective; ELBO + InfoNCE cover the reusable parts |
| DirectAU recommendation loss | Score < 30; limited evergreen / interview value vs BPR |
| Straight-Through Estimator alone | Score < 30; better taught inside Gumbel-Softmax |
| Neural ODE adjoint sensitivity | Implementation burden exceeds portfolio-fit authenticity gate |
| InfoNCE aliases / CLIP-only framings | Duplicate of queued foundation `info_nce` |
| Hardware kernels / benchmark leaderboards / prompt tips | Explicit discovery-policy rejects |

---

# Repository Coverage

| Area | Coverage |
|------|----------|
| Transformer Core | Strong intent, weak execution: only Attention Scaling shipped; Softmax/MHA/LN/Residuals still gaps |
| Optimization | Queued Adam + Weight Decay; no shipped modules |
| Loss Functions | Queued CE/KL, Focal, InfoNCE; emerging CTC, BPR, Gumbel |
| Diffusion | Queued DDPM; emerging ELBO, score matching, flow matching, Sinkhorn |
| Reinforcement Learning | Foundation REINFORCE/KL-RL still unqueued; emerging log-derivative + importance sampling seeds |
| Computer Vision | Emerging ViT patch embedding only |
| Representation Learning | Queued InfoNCE; emerging VICReg, Barlow Twins, JEPA |
| Recommendation Systems | Emerging two-tower + BPR |
| World Models | Emerging JEPA + Kalman filter |
| Audio / Speech | Emerging CTC + mel filterbank |
| Graph ML | Emerging message passing |
| Quantitative Finance | Emerging Black-Scholes PDE |
| Causal Inference | Emerging IPW; Neyman/AIPW blocked until IPW ships |

---

# Notes

- Suggested next module remains Softmax Jacobian (same as W31-W35) because it is still unbuilt and still the highest continuity unlock.
- New topics merged into `topics.json` this week: revalidated W31-W35 emerging set that never landed on main, plus `log_derivative_trick`, `importance_sampling`, `gaussian_mixture_em`, `barlow_twins`.
- `neyman_orthogonal_score` scored 30 but was blocked (not merged) until IPW exists as a shipped/queued prerequisite foundation.
- Existing manual foundation topics left untouched (no renames, deletes, or status edits).
- `foundation_curriculum.json` and `interest_domains` were not modified.
- Sources unavailable: X/Twitter (Tier 5) not queried; OpenAI research index reachable but yielded formal-math product posts rather than reusable ML mechanisms. NeurIPS/ICLR proceedings, lab/community blogs, and arXiv HTML were usable.
- Diversity preference applied only among ≥30 candidates; Softmax still wins over domain-diversifying emerging topics for the single weekly build recommendation.
