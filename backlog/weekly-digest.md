# Weekly AI Math Digest

Generated: 2026-10-04 (ISO 2026-W40)

---

# Suggested Next Module

## Softmax Jacobian & Backpropagation (`softmax_jacobian`)

Overall Score: **39 / 40**

Reason:

Only `attention_scaling` has three-layer evidence. Softmax Jacobian is the live hinge on the transformer spine: Multi-Head Attention, causal masks, and FlashAttention all depend on it. LayerNorm and Adam can match the raw score, but Softmax uniquely continues the only completed module and unlocks the largest set of foundation successors this week.

Prerequisites Satisfied

- ✅ Attention Scaling Factor (`attention_scaling`) shipped under `modules/01_attention_scaling/`
- ✅ Softmax as a probability map is assumed by Module 01's scaled-dot-product derivation

Unlocks

- Multi-Head Attention
- Causal / attention mask structure
- FlashAttention tiling identity path
- Modern Hopfield energy retrieval (`modern_hopfield_energy`)
- Temperature scaling / sparsemax-class normalizers later

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
|--------|-------|
| Completed foundations | 1 / 15 backlog foundations: `attention_scaling` only (`.md` + `.jpg` + `.ipynb`) |
| Queued foundations | Softmax → MHA → RoPE / KV Cache → FlashAttention; LayerNorm → SwiGLU; Adam → Weight Decay; CE/KL → Focal / InfoNCE; DDPM; LoRA |
| Domain coverage | Shipped: Transformer Core only. Backlog seeds exist across many domains but nothing outside Transformers is implemented |
| Curriculum continuity | Broken after Module 01 until Softmax Jacobian ships |
| Prerequisite graph | Softmax is the critical cut vertex before MHA, masks, KV, Flash, and Hopfield |
| Implementation backlog | 14 foundation + 58 emerging topics with `github: todo` |
| Blog backlog | `attention_scaling` blog still `wip`; all other blogs `todo` |
| Research backlog | All non-01 research statuses remain `todo` |

**Single largest curriculum weakness:** Softmax Jacobian is missing, so the transformer spine cannot advance and continuity from the only shipped module is stalled.

**Underrepresented ML domains (no shipped modules):** Vision, Representation Learning, Diffusion, RL, Recommendation, Audio, World Models, Graph ML, Quantitative Finance, Causal Inference.

---

# Foundation Gaps

Remaining foundation topics in `topics.json`, scored with `scoring.md`. Softmax preferred for continuity even when LayerNorm/Adam tie on raw score.

| Rank | Topic | Score | Why Now | Unlocks |
|------|------:|--------|----------|----------|
| 1 | Softmax Jacobian (`softmax_jacobian`) | 39 | Continues Module 01; prereq satisfied | MHA, masks, Flash path, Hopfield |
| 2 | Layer Normalization (`layernorm`) | 39 | Parallel stabilizer track; no hard prereq | RMSNorm, Pre/Post-LN, SwiGLU |
| 3 | Adam from First Principles (`adam_optimizer`) | 39 | Interview staple; no hard prereq | Weight decay, schedules, later Muon |
| 4 | Residual connections (`f07`, curriculum-only) | 38 | Missing bridge beside LN for deep nets | Pre/Post-LN, Peri-LN / HybridNorm later |
| 5 | Multi-Head Attention (`multi_head_attention`) | 38 | Spine unlock, but waits on Softmax | RoPE, KV Cache, GQA, Flash |

Other high-scoring foundations deferred this week: DDPM (38, portfolio-strong but continuity weaker), CE vs KL (37), LoRA (36), InfoNCE (36, needs CE/KL), Focal Loss (needs CE/KL), Weight Decay (needs Adam), RoPE / KV / Flash / SwiGLU (blocked on earlier spine nodes).

---

# Missing Links

Highest-impact conceptual holes (often higher priority than new research):

1. **Softmax Jacobian** - live hinge after Attention Scaling
2. **Residual connections** (`f07`) - in `foundation_curriculum.json` but absent from `topics.json`
3. **Causal / attention mask** (`f08`) - autoregressive legality bridge before KV / Flash stories
4. **ELBO + reparameterization** before deep DDPM / VAE / RSSM work (emerging seeds exist; not shipped)
5. **Score matching + Langevin** beside DDPM / flow matching
6. **Log-derivative + Bellman + TD / Advantage** before REINFORCE / PPO / GRPO (emerging seeds exist)
7. **Bradley-Terry before DPO / RLHF preference posts** (merged this week as emerging)
8. **Itô's Lemma** before first-principles Black-Scholes depth
9. **STFT before Mel filterbank**
10. **Graph Laplacian beside message passing**
11. **Wasserstein before Sinkhorn-only OT treatments**

---

# Emerging Candidates

Accepted this week after `scoring.md` hard gates. Prior W31-W39 emerging set revalidated and re-merged (still absent from `main`). New W40 accepts below.

| Topic | Domain | Score | Confidence | Why Interesting | Blocked On |
|--------|--------|------:|------------|-----------------|------------|
| bradley_terry_preference | Preference / RLHF | 39 | High | Pairwise sigmoid preference model; unlocks DPO and reward-model interviews | - |
| direct_preference_optimization | Preference / RLHF | 37 | High | Closed-form policy reparameterization; Z(x) cancels under BT | bradley_terry + CE/KL |
| rejection_sampling | Monte Carlo | 34 | High | Exact sampling with envelope proposals; pairs with MH / IS | - |
| alternating_least_squares | Recommendation | 34 | High | Closed-form biconvex MF updates; RecSys interview staple | - |
| f_divergence | Info Theory | 34 | High | Unifies KL / JS / α-divergences for generative and RLHF math | CE vs KL |
| entropy_regularized_rl | Reinforcement Learning | 34 | High | Soft optimality / MaxEnt policy ∝ exp(Q/α) | log-derivative + Bellman |
| hamiltonian_monte_carlo | Monte Carlo | 33 | Medium | Gradient-informed MCMC via leapfrog + Metropolis | MH + Langevin |
| modern_hopfield_energy | Associative Memory | 32 | Medium | Energy whose retrieval update recovers softmax attention | Softmax Jacobian |
| rssm_variational_bound | World Models | 31 | Medium | Dreamer-style recurrent state-space ELBO | ELBO + reparameterization |
| causal_mediation_effects | Causal Inference | 31 | Medium | Natural direct/indirect effect decomposition | back-door adjustment |
| canonical_correlation_analysis | Representation Learning | 30 | Medium | Two-view correlation via cross-covariance eigenproblem | - |

---

# Blocked Candidates

Worth revisiting after prerequisites. **Not merged** into `topics.json`.

| Topic | Waiting For |
|--------|-------------|
| Peri-LN / HybridNorm / SpanNorm / SiameseNorm / DeepNorm | LayerNorm + residual connections |
| MoE routers (STAR / AAR / load-balance variants) | MoE routing foundation (`f34`) |
| GQA / MQA | Multi-Head Attention + KV Cache |
| FlashAttention v2 / v3 | FlashAttention |
| YaRN / ClockRoPE / RoPE variants | RoPE |
| QLoRA / LoRA+ / DoRA | LoRA |
| Muon / Newton-Schulz optimizer variants | Adam |
| Norm×Direction linear attention / Monarch / CEDAR / ARM / MARCH / Slim Attention / attention sinks | MHA (+ KV where memory-bound) |
| Multi-token / differential / gated / hierarchical attention | Multi-Head Attention |
| Consistency models / CFG / DDIM | DDPM forward process |
| Rectified flow / OT-CFM / Contrastive FM | Flow matching (+ OT where claimed) |
| AIPW / Neyman orthogonal scores | Inverse propensity weighting |
| GAT / Graph Attention | Message passing (+ Softmax/MHA intuition) |
| Particle filter / RTS smoother | Kalman filter |
| Black-Scholes Greeks | Black-Scholes PDE + Itô |
| Speculative decoding (as emerging) | Already foundation `f35`; also needs sampling + KV |
| SIGReg / Causal-JEPA | JEPA predictive objective |
| Scalable-Softmax / length-aware softmax normalizers | Softmax Jacobian |
| ZeroS / zero-sum linear attention | Softmax + MHA (+ LN for stability claims) |

---

# Rejected This Week

| Topic | Reason |
|--------|--------|
| RouteLLM / BEST-Route / GraphRouter | Product-style LLM routers; not a reusable first-principles mathematical mechanism |
| Nested Learning (continual-learning paradigm) | Architectural meta-framework; fails clean standalone derivation + small PyTorch module fit |
| Adjoint Sampling / Adjoint Matching stack | Composite diffusion-sampler system; score <30 for interview/evergreen/portfolio fit as a single module |
| I-CON unified representation loss | Meta-unification of many methods; not one implementable mechanism |
| Sparsemax / Entmax | Score <30 until Softmax ships; thin portfolio value vs Softmax Jacobian |
| Soft-DTW | Score <30; niche sequence metric |
| Derf / DyT normalization-free activations | Trend coupling with Muon; fails evergreen + authenticity gates vs LayerNorm/RMSNorm path |
| FlashPairformer / Triton kernel posts | Hardware kernels, not math modules |
| gpt-oss / model release writeups | Product / checkpoint announcements |
| 1-shot RLVR / SPARKLE / evaluation frames | Benchmark / eval product frames |
| Prompt / Declarative Attention protocols | Prompt engineering |
| InfoNCE aliases / CLIP rebrands | Duplicate of foundation `info_nce` |
| Straight-Through Estimator alone | Score <30; weak standalone portfolio module |
| Neural ODE adjoint | Previously rejected; still fails effort/portfolio bar vs clearer mechanisms |
| AlphaEvolve / Deep Think discovery posts | Tooling / agent demos, not mechanisms |

---

# Repository Coverage

| Area | Coverage |
|------|----------|
| Transformer Core | Shipped: Attention Scaling. Queued: Softmax, LN, MHA. Emerging: QK-Norm, Hopfield |
| Optimization | Queued: Adam, Weight Decay. Emerging: Natural Gradient, Polyak EMA, Hutchinson |
| Loss Functions | Queued: CE/KL, Focal, InfoNCE. Emerging: CTC, BPR, VICReg/Barlow/BYOL, MMD, f-divergence |
| Diffusion | Queued: DDPM. Emerging: Score matching, Flow matching, Langevin, ELBO, reparameterization |
| Reinforcement Learning | Emerging: log-derivative, Bellman, TD, Advantage, GAE, GRPO-style group advantage, PPO clip, entropy-regularized RL, DPO path |
| Computer Vision | Emerging: ViT patch embedding, spectral norm, Fourier features, FiLM |
| Representation Learning | Emerging: VICReg, Barlow, BYOL, JEPA, sparse dictionary, CCA, MMD |
| Recommendation Systems | Emerging: Two-tower retrieval, BPR, Alternating Least Squares |
| World Models | Emerging: JEPA, RSSM variational bound |
| Audio / Speech | Emerging: STFT → Mel, CTC |
| Graph ML | Emerging: Message passing, Graph Laplacian |
| Quantitative Finance | Emerging: Black-Scholes PDE, Itô lemma |
| Causal Inference | Emerging: IPW, back-door, front-door, mediation effects |
| Monte Carlo / Uncertainty | Emerging: MH, importance sampling, rejection sampling, HMC, control variates, conformal prediction |

---

# Notes

- Suggested next module remains **Softmax Jacobian** (same objective ranking as W32-W39) because Module 01 is still the only shipped artifact and Softmax is still the continuity cut vertex.
- New topics merged into `topics.json` this week: `bradley_terry_preference`, `direct_preference_optimization`, `rejection_sampling`, `alternating_least_squares`, `f_divergence`, `entropy_regularized_rl`, `hamiltonian_monte_carlo`, `modern_hopfield_energy`, `rssm_variational_bound`, `causal_mediation_effects`, `canonical_correlation_analysis`.
- Re-merged (still absent from `main`): full W31-W39 emerging set from `qk_norm` through `sparse_dictionary_learning`, with Mel requiring STFT; GAE requiring TD+Advantage; Langevin requiring score matching; front-door requiring back-door; PPO clip requiring Advantage + log-derivative; group-relative advantage requiring Advantage.
- Existing topics skipped (no renames, deletions, or manual status edits): all foundation entries `01`-`15`.
- `foundation_curriculum.json` and `interest_domains` untouched.
- Domains explored: Transformers, Vision, Representation Learning, Diffusion, RL, Recommendation, Audio, World Models, Graph ML, Quantitative Finance, Causal Inference, Monte Carlo, Preference Learning, Optimization.
- Sources unavailable: X/Twitter (Tier 5) unused (optional). OpenAI / Anthropic / DeepMind public surfaces were mostly product, interpretability, or agent-demo posts; only reusable mechanisms were retained.
