# Weekly AI Math Digest

Generated: 2026-09-13 (2026-W37)

---

# Suggested Next Module

## Softmax Jacobian & Backpropagation (`softmax_jacobian`)

Overall Score: 39 / 40

Reason:

Module 01 (`attention_scaling`) is the only shipped three-layer artifact. Softmax Jacobian is the immediate foundation bridge on that path: it derives `diag(p) - ppᵀ`, explains gradient flow through attention weights, and is a hard prerequisite for Multi-Head Attention and FlashAttention. LayerNorm and Adam can match the raw score, and DDPM / LoRA are close, but Softmax uniquely maximizes curriculum continuity from the only completed module. If the author builds only one module this week, this is the one that most improves the repository.

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
| Domain coverage | Almost entirely Transformer Core on the critical path; other domains exist only as queued foundations or emerging seeds restored this week |
| Curriculum continuity | Fragile: one shipped node; Softmax is the missing hinge before the MHA spine |
| Prerequisite graph | Softmax blocks MHA, which blocks RoPE, KV Cache, GQA, and FlashAttention |
| Implementation backlog | 14 foundation topics still `github: todo`; emerging queue re-seeded because W31-W36 draft PRs never landed on main |
| Blog backlog | Attention Scaling blog WIP; all later topics unset |
| Research backlog | Attention Scaling research completed; all later topics unset |

Single largest curriculum weakness: Softmax Jacobian is still unbuilt, so the transformer spine cannot advance past Attention Scaling.

Underrepresented ML domains (shipped evidence): Vision, Representation Learning, Diffusion, RL, Recommendation, Audio, World Models, Graph ML, Quant Finance, and Causal Inference all remain at zero shipped modules.

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
4. ELBO + reparameterization trick before deep DDPM reverse-process / VAE work - seeded this week as `elbo_variational_bound` and `reparameterization_trick`.
5. Score matching beside DDPM / flow matching - closes the generative modeling triangle; seeded as `score_matching`.
6. Log-derivative trick and Bellman expectation before REINFORCE / RLHF-style objectives - seeded as `log_derivative_trick` and `bellman_expectation`.
7. Short-time Fourier transform before Mel filterbank - STFT now precedes Mel in the emerging graph.

---

# Emerging Candidates

Accepted only if score ≥ 30, portfolio fit gates pass, and prerequisites are satisfiable from current/queued foundations (not advanced variants of unbuilt modules).

| Topic | Domain | Score | Confidence | Why Interesting | Blocked On |
|--------|--------|------:|------------|-----------------|------------|
| reparameterization_trick | Generative Models | 39 | High | Pathwise Gaussian reparameterization; pairs with ELBO for VAEs | - |
| elbo_variational_bound | Diffusion / Generative | 37 | High | Core latent-variable identity; unlocks VAEs and disciplined DDPM reading | - |
| flow_matching | Diffusion / Generative | 36 | High | Simulation-free vector-field regression; evergreen alternative to score SDEs | - |
| score_matching | Diffusion / Generative | 36 | High | Denoising score matching links noise prediction to ∇ log p | - |
| message_passing | Graph ML | 36 | High | GNN backbone aggregation math | - |
| log_derivative_trick | Reinforcement Learning | 36 | High | ∇ log π identity; foundation for REINFORCE / policy gradients | - |
| bellman_expectation | Reinforcement Learning | 36 | High | V = R + γP V recursive identity; DP/TD gateway | - |
| gumbel_softmax | Representation / Discrete | 35 | High | Reparameterization for categorical latents; widely reused | - |
| vit_patch_embedding | Vision | 35 | High | Patchify + linear projection as vision tokenization | - |
| qk_norm | Transformers | 34 | High | Per-vector Q/K normalization stabilizing attention logits | attention_scaling (satisfied) |
| ctc_loss | Audio / Speech | 34 | High | Alignment-free sequence loss via dynamic programming | - |
| two_tower_retrieval | Recommendation / Embeddings | 34 | High | Dual-encoder similarity learning mechanism | - |
| black_scholes_pde | Quantitative Finance | 34 | High | Closed-form PDE derivation with hedge argument | - |
| kalman_filter | World Models / Signal | 34 | High | Predict-update Gaussian filtering; transferable state estimation | - |
| importance_sampling | Foundations / Inference | 34 | High | Change-of-measure estimator across RL, eval, and Monte Carlo | - |
| gaussian_mixture_em | Foundations | 34 | High | EM as alternating E-step responsibilities and M-step MLE | - |
| natural_gradient | Optimization | 34 | High | Fisher-information preconditioned step; information geometry | - |
| inverse_propensity_weighting | Causal Inference | 33 | High | Reweighting identity for observational bias | - |
| jepa_predictive_objective | World Models | 33 | Medium | Predict-in-embedding space without pixel reconstruction | - |
| bpr_ranking_loss | Recommendation | 33 | High | Pairwise logistic ranking from implicit feedback | - |
| short_time_fourier_transform | Audio / Speech | 33 | High | Windowed DFT analysis; prerequisite bridge into Mel features | - |
| mel_filterbank | Audio / Speech | 32 | High | Mel-scale triangular filter math under STFT features | STFT (queued emerging) |
| sinkhorn_optimal_transport | Diffusion / OT | 32 | Medium | Entropic OT iterations; couples to flow / transport paths | - |
| hutchinson_trace_estimator | Numerical Linear Algebra | 32 | Medium | Stochastic trace probes; reusable in densities and curvature | - |
| barlow_twins | Representation Learning | 31 | Medium | Cross-correlation redundancy reduction; distinct from VICReg | - |
| spectral_normalization | Vision / Stability | 31 | Medium | Power-iteration Lipschitz constraint on layer weights | - |
| vicreg | Representation Learning | 30 | Medium | Variance-invariance-covariance collapse prevention | - |
| byol_bootstrap | Representation Learning | 30 | Medium | EMA target bootstrap SSL without negatives | - |

---

# Blocked Candidates

Topics worth revisiting after prerequisite modules are complete. Not merged into `topics.json`.

| Topic | Waiting For |
|--------|-------------|
| Grouped Query / Multi-Query Attention | Multi-Head Attention + KV Cache |
| FlashAttention v2 / v3 / IO kernel variants | FlashAttention |
| YaRN / Long-RoPE variants | RoPE |
| QLoRA / LoRA+ / DoRA | LoRA |
| Muon / Newton-Schulz orthogonalized updates | Adam |
| Peri-LN / HybridNorm / DeepNorm placement variants | LayerNorm + Residual connections |
| Multi-Token Attention / gated / differential attention | Multi-Head Attention |
| Compressed / Heavily Compressed / DeepSeek Sparse Attention | Multi-Head Attention + KV Cache |
| Manifold-Constrained Hyper-Connections (mHC) | Residual connections |
| KERN / Nadaraya-Watson MoE routers | Mixture-of-Experts routing foundation |
| Consistency models / sCM distillation | DDPM forward process |
| Rectified flow / OT-CFM / semidiscrete OT-FM variants | Flow Matching |
| SIGReg / Causal-JEPA / LeJEPA regularizers | JEPA predictive objective |
| Graph Attention Networks (GAT) | Message passing |
| Black-Scholes Greeks taxonomy | Black-Scholes PDE |
| AIPW / doubly robust estimators | Inverse propensity weighting |
| Neyman orthogonal score | Inverse propensity weighting |
| Speculative decoding acceptance math | Already foundation `f35`; needs sampling + KV Cache |
| Particle filter | Kalman filter |

---

# Rejected This Week

| Topic | Reason |
|--------|--------|
| Sparsemax | Score 28 (<30); better after Softmax Jacobian ships as a projection companion |
| Soft-DTW | Score 26; high implementation cost / niche interview value vs CTC |
| DeepSeek / product model stacks | Model release + composite architecture; not a single reusable mechanism |
| HybridNorm / Peri-LN as emerging merges | Prerequisite gate: need LayerNorm + residuals first (listed under Blocked) |
| Multi-Token Attention | Architectural attention variant before MHA foundation |
| FlashAttention-3 | Hardware/kernel variant before FlashAttention |
| OpenAI / Anthropic formal-math and product posts | Not reusable ML mechanisms for this curriculum (extended thinking, GPQA scaling) |
| Scaling-laws blog math alone | Macro empirical fitting; weak standalone PyTorch / canvas module |
| InfoNCE aliases / CLIP-only framings | Duplicate of queued foundation `info_nce` |
| Straight-Through Estimator alone | Score < 30; better taught inside Gumbel-Softmax |
| Neural ODE adjoint sensitivity | Implementation burden exceeds portfolio-fit authenticity gate |
| DirectAU recommendation loss | Score < 30; limited evergreen / interview value vs BPR |
| Hardware kernels / benchmark leaderboards / prompt tips | Explicit discovery-policy rejects |

---

# Repository Coverage

| Area | Coverage |
|------|----------|
| Transformer Core | Strong intent, weak execution: only Attention Scaling shipped; Softmax/MHA/LN/Residuals still gaps |
| Optimization | Queued Adam + Weight Decay; emerging Natural Gradient |
| Loss Functions | Queued CE/KL, Focal, InfoNCE; emerging CTC, BPR, Gumbel |
| Diffusion | Queued DDPM; emerging ELBO, reparameterization, score matching, flow matching, Sinkhorn |
| Reinforcement Learning | Emerging log-derivative + Bellman expectation + importance sampling; foundation REINFORCE still unqueued in topics |
| Computer Vision | Emerging ViT patch embedding + spectral normalization |
| Representation Learning | Queued InfoNCE; emerging VICReg, Barlow Twins, BYOL bootstrap, JEPA |
| Recommendation Systems | Emerging two-tower + BPR |
| World Models | Emerging JEPA + Kalman filter |
| Audio / Speech | Emerging STFT → Mel filterbank + CTC |
| Graph ML | Emerging message passing |
| Quantitative Finance | Emerging Black-Scholes PDE |
| Causal Inference | Emerging IPW; Neyman/AIPW blocked until IPW ships |

---

# Notes

- Suggested next module remains Softmax Jacobian (same as W31-W36) because it is still unbuilt and still the highest continuity unlock.
- W31-W36 emerging merges still had not landed on `main`; this week revalidates and re-merges that set, adds STFT as Mel's prerequisite, and merges new W37 candidates: `reparameterization_trick`, `bellman_expectation`, `natural_gradient`, `hutchinson_trace_estimator`, `spectral_normalization`, `byol_bootstrap`.
- Existing manual foundation topics left untouched (no renames, deletes, or status edits).
- `foundation_curriculum.json` and `interest_domains` were not modified.
- Sources unavailable: X/Twitter (Tier 5) not queried. OpenAI/Anthropic research surfaces were reachable but mostly returned product, formal-math, or system posts rather than reusable ML mechanisms. NeurIPS/ICLR proceedings, Meta/DeepMind-adjacent mechanism writeups, Lil'Log, and arXiv HTML were usable.
- Diversity preference applied only among ≥30 candidates; Softmax still wins over domain-diversifying emerging topics for the single weekly build recommendation.
