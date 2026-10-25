# Weekly AI Math Digest

Generated: 2026-10-25 (ISO 2026-W43)

---

# Suggested Next Module

## Softmax Jacobian & Backpropagation (`softmax_jacobian`)

Overall Score: **39 / 40**

Reason:

Only `attention_scaling` has three-layer evidence. Softmax Jacobian is the live hinge on the transformer spine: Multi-Head Attention, causal masks, online softmax, and FlashAttention all depend on it. LayerNorm and Adam can match the raw score, but Softmax uniquely continues the only completed module and unlocks the largest set of foundation successors this week. If the author builds only one module, this is unquestionably the highest long-term value choice.

Prerequisites Satisfied

- ✅ Attention Scaling Factor (`attention_scaling`) shipped under `modules/01_attention_scaling/`
- ✅ Softmax as a probability map is assumed by Module 01's scaled-dot-product derivation

Unlocks

- Multi-Head Attention
- Causal / attention mask structure
- Online Softmax → FlashAttention tiling identity path
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
| Domain coverage | Shipped: Transformer Core only. Backlog seeds span preference learning, bandits/RecSys, SSM memory, optimization geometry, causal IPS, Schrödinger bridges, CRPS/pinball forecasting, WPO, and prior W31-W42 domains |
| Curriculum continuity | Broken after Module 01 until Softmax Jacobian ships |
| Prerequisite graph | Softmax is the critical cut vertex before MHA, masks, KV, online softmax, Flash, and Hopfield |
| Implementation backlog | 14 foundation + 82 emerging topics with `github: todo` |
| Blog backlog | `attention_scaling` blog still `wip`; all other blogs `todo` |
| Research backlog | All non-01 research statuses remain `todo` |

**Single largest curriculum weakness:** Softmax Jacobian is missing, so the transformer spine cannot advance and continuity from the only shipped module is stalled.

**Underrepresented ML domains (no shipped modules):** Vision, Representation Learning, Diffusion, RL, Recommendation, Audio, World Models, Graph ML, Quantitative Finance, Causal Inference.

---

# Foundation Gaps

Remaining foundation topics evaluated with `scoring.md`. Softmax preferred for continuity even when LayerNorm/Adam tie on raw score. `foundation_curriculum.json` was not modified.

| Rank | Topic | Score | Why Now | Unlocks |
|------|------:|--------|----------|----------|
| 1 | Softmax Jacobian (`softmax_jacobian`) | 39 | Continues Module 01; prereq satisfied | MHA, masks, online softmax, Flash path, Hopfield |
| 2 | Layer Normalization (`layernorm`) | 39 | Parallel stabilizer track; no hard prereq | RMSNorm, Pre/Post-LN, SwiGLU |
| 3 | Adam from First Principles (`adam_optimizer`) | 39 | Interview staple; no hard prereq | Weight decay, schedules, later Muon |
| 4 | Residual connections (`f07`, curriculum-only) | 38 | Missing bridge beside LN for deep nets | Pre/Post-LN, Peri-LN / HybridNorm later |
| 5 | Multi-Head Attention (`multi_head_attention`) | 38 | Spine unlock, but waits on Softmax | RoPE, KV Cache, GQA, Flash |

Scoring notes (0-5 each category → /40): Softmax / LayerNorm / Adam each land at Math 5, Impl 5, Viz 5, Interview 5, Industry 5, Evergreen 5, Educational 5, Portfolio 4 (=39). Residuals and MHA score 38 (slightly lower portfolio or unlock-timing penalty while Softmax is absent).

Other high-scoring foundations deferred this week: DDPM (38, portfolio-strong but continuity weaker), CE vs KL (37), LoRA (36), InfoNCE (36, needs CE/KL), Focal Loss (needs CE/KL), Weight Decay (needs Adam), RoPE / KV / Flash / SwiGLU (blocked on earlier spine nodes).

---

# Missing Links

Highest-impact conceptual holes (often higher priority than new research):

1. **Softmax Jacobian** - live hinge after Attention Scaling
2. **Residual connections** (`f07`) - in `foundation_curriculum.json` but absent from `topics.json`
3. **Causal / attention mask** (`f08`) - autoregressive legality bridge before KV / Flash stories
4. **Online Softmax** before treating FlashAttention as a black-box kernel (seeded; waits on Softmax)
5. **ELBO + reparameterization** before deep DDPM / VAE / RSSM work (emerging seeds exist; not shipped)
6. **Score matching + Langevin** beside DDPM / flow matching / Schrödinger bridge
7. **Log-derivative + Bellman + TD / Advantage** before REINFORCE / PPO / GRPO / DPG / RWR (emerging seeds exist)
8. **Bradley-Terry before DPO**; **CE/KL before KTO / f-divergence / Best-of-N KL / Jeffreys**
9. **Bregman divergence before Mirror Descent** (seeded as a linked pair)
10. **Natural Gradient + Wasserstein + Advantage before WPO**
11. **Itô's Lemma** before first-principles Black-Scholes depth
12. **IPW before SNIPS / AIPW**
13. **STFT before Mel filterbank**
14. **Graph Laplacian before spectral clustering**
15. **Wasserstein / Sinkhorn before Schrödinger-bridge-only OT treatments**
16. **HiPPO before S4 / Elastic Memory / long-context SSM variants**
17. **Momentum SGD before Nesterov** (Nesterov seeded this week as the lookahead variant)

---

# Emerging Candidates

Accepted after `scoring.md` hard gates. Prior W31-W42 emerging set revalidated and re-merged (still absent from `main`). New W43 accepts below.

| Topic | Domain | Score | Confidence | Why Interesting | Blocked On |
|--------|--------|------:|------------|-----------------|------------|
| nesterov_accelerated_gradient | Optimization | 35 | High | Lookahead correction on heavy-ball momentum; evergreen convex-accel identity | - |
| deterministic_policy_gradient | Reinforcement Learning | 34 | High | ∇_a Q policy path for continuous control; Silver DPG identity | Advantage |
| reward_weighted_regression | Reinforcement Learning | 33 | High | Weighted MLE policy improvement; bridge to reward-weighted diffusion finetuning | Log-derivative |
| continuous_ranked_probability_score | Quantitative Finance | 32 | High | Proper scoring rule; MAE special case; weather/finance ensemble staple | - |
| pinball_quantile_loss | Quantitative Finance | 31 | High | Asymmetric absolute loss for quantile regression | - |
| jeffreys_divergence | Loss / Alignment | 31 | Medium | Symmetric KL sum; closed-form role in KL-budget alignment limits | CE vs KL |
| welford_online_variance | Foundations / Systems | 31 | High | One-pass stable mean/M2; streaming BatchNorm / Flash numerical hinge | - |
| wasserstein_policy_optimization | Reinforcement Learning | 30 | Medium | ICML 2025; project Wasserstein policy flow into Fisher parameter step | Wasserstein + Natural Gradient + Advantage |

---

# Blocked Candidates

Worth revisiting after prerequisites. **Not merged** into `topics.json`.

| Topic | Waiting For |
|--------|-------------|
| Peri-LN / HybridNorm / SpanNorm / SimpleNorm / SiameseNorm / DeepNorm / Mix-LN / nGPT dynamics papers | LayerNorm + residual connections |
| MoE routers (ProbMoE / STAR / AAR / orthogonality+variance routing losses) | MoE routing foundation (`f34`) |
| GQA / MQA / MLA / KV-sharing architecture variants | Multi-Head Attention + KV Cache |
| FlashAttention v2 / v3 | FlashAttention |
| YaRN / ClockRoPE / RoPE variants | RoPE |
| QLoRA / LoRA+ / DoRA | LoRA |
| Muon / Newton-Schulz optimizer variants | Adam |
| Norm×Direction linear attention / Monarch / CEDAR / ARM / MARCH / Slim Attention / attention sinks | MHA (+ KV where memory-bound) |
| Kernel / linear attention (Performer FAVOR+) | Multi-Head Attention (+ Softmax) |
| Multi-token / differential / gated / hierarchical / verified sparse attention (vAttention) | Multi-Head Attention (+ Softmax) |
| α-entmax / AdaSplash sparse attention | Softmax Jacobian (+ MHA) |
| BalanceKV / streaming attention approximation via discrepancy theory | Multi-Head Attention + KV Cache |
| Consistency models / CFG / DDIM | DDPM forward process |
| Rectified flow / OT-CFM / Contrastive FM / Source-guided FM / Topological FM / Bures-Wasserstein FM / Semidiscrete OT-FM | Flow matching (+ Wasserstein / Sinkhorn / Graph Laplacian where claimed) |
| Moment Matching Distillation / RMMD stacks | DDPM (+ score matching / MMD) |
| Counterfactual dynamic OT maps | Back-door + flow matching + Wasserstein |
| AIPW / Neyman orthogonal scores | Inverse propensity weighting (+ ideally SNIPS intuition) |
| GAT / Graph Attention | Message passing (+ Softmax/MHA intuition) |
| Particle filter / RTS smoother / SMC / EKF | Kalman filter |
| Black-Scholes Greeks | Black-Scholes PDE + Itô |
| Speculative decoding (as emerging) | Already foundation `f35`; also needs sampling + KV |
| SIGReg / Causal-JEPA | JEPA predictive objective |
| Scalable-Softmax / length-aware softmax / ZeroS | Softmax Jacobian (+ MHA for ZeroS) |
| GraphAE / representation-aware advantage estimators | Advantage + message passing |
| GSPO / DAPO / CISPO / Dr. GRPO objective tweaks | Advantage + PPO clip / group-relative advantage |
| SANTA++ / representative-key attention sampling | MHA + KV Cache + importance sampling |
| Sparse-plus-low-rank quasi-Newton Sinkhorn solvers | Sinkhorn (+ conjugate gradient / Newton tooling) |

---

# Rejected This Week

| Topic | Reason |
|--------|--------|
| Limitations-of-softmax / Normalization-in-Attention-Dynamics theory papers | Diagnostic analysis of existing normalizers, not a new reusable implementable mechanism |
| HybridNorm / Peri-LN as emerging merges | Prerequisite gate: need LayerNorm + residuals first (listed under Blocked) |
| BatchNorm / RMSNorm / temperature / log-sum-exp as emerging | Already in `foundation_curriculum.json` (`f04`, `f05`, `f14`, `f15`); novelty gate |
| AdaLayerNorm as emerging | Thin FiLM + LayerNorm variant; FiLM already seeded |
| Linearly-solvable MDP / KL-control framing alone | Score <30 for standalone portfolio fit without a tighter identity |
| Moment Matching Distillation / RMMD product stacks | Composite distillation+RL system; fails clean 100-300 line first-principles module |
| Diffusion Controller / discrete diffusion policy product papers | Composite systems; extractable pieces already covered (Mirror Descent, RWR, score matching) |
| Continuous batching serving systems | Systems scheduling, not a mathematical mechanism module |
| Looped / recursive transformer architecture tourism | Model-release architecture variants |
| Kuramoto oscillatory neurons | Niche dynamical unit; weak interview/industry vs evergreen alternatives |
| Sparsemax / Entmax alone | Score <30 or weak portfolio until Softmax Jacobian ships |
| IPO / thin DPO regularizers | Prefer Bradley-Terry → DPO → KTO path |
| InfoNCE aliases / CLIP rebrands | Duplicate of foundation `info_nce` |
| Prompt / Declarative Attention protocols | Prompt engineering |
| Model releases / benchmarks / hardware kernels | Outside discovery policy |

---

# Repository Coverage

| Area | Coverage |
|------|----------|
| Transformer Core | Shipped: Attention Scaling. Queued: Softmax, LN, MHA. Emerging: QK-Norm, Hopfield, Online Softmax |
| Optimization | Queued: Adam, Weight Decay. Emerging: Momentum, Nesterov, EMA, Natural Gradient, Polyak, Hutchinson, Bregman, Mirror Descent, Conjugate Gradient |
| Loss Functions | Queued: CE/KL, Focal, InfoNCE. Emerging: CTC, BPR, Hinge, Pinball, VICReg/Barlow/BYOL, MMD, f-divergence, Jeffreys |
| Diffusion | Queued: DDPM. Emerging: Score matching, Flow matching, Langevin, ELBO, reparameterization, Schrödinger bridge |
| Reinforcement Learning | Emerging: log-derivative, Bellman, TD, Advantage, GAE, group advantage, PPO clip, DPG, RWR, WPO, entropy-regularized RL, DPO path, Best-of-N KL |
| Computer Vision | Emerging: ViT patch embedding, spectral norm, Fourier features, FiLM |
| Representation Learning | Emerging: VICReg, Barlow, BYOL, JEPA, sparse dictionary, CCA, MMD, Information Bottleneck |
| Recommendation Systems | Emerging: Two-tower, BPR, ALS, Thompson Sampling, UCB |
| World Models | Emerging: JEPA, RSSM variational bound, HiPPO polynomial projection, Schrödinger bridge |
| Audio / Speech | Emerging: STFT → Mel, CTC |
| Graph ML | Emerging: Message passing, Graph Laplacian, Spectral Clustering |
| Quantitative Finance | Emerging: Black-Scholes PDE, Itô lemma, CRPS, Pinball quantile loss |
| Causal Inference | Emerging: IPW, SNIPS, back-door, front-door, mediation effects |
| Monte Carlo / Uncertainty | Emerging: MH, importance sampling, rejection sampling, HMC, control variates, conformal prediction, Welford online variance |
| Preference Learning | Emerging: Bradley-Terry, DPO, Kahneman-Tversky Optimization, Best-of-N KL, Jeffreys divergence |

---

# Notes

- Suggested next module remains **Softmax Jacobian** (same objective ranking as W32-W42) because Module 01 is still the only shipped artifact and Softmax is still the continuity cut vertex.
- New topics merged into `topics.json` this week: `nesterov_accelerated_gradient`, `deterministic_policy_gradient`, `reward_weighted_regression`, `continuous_ranked_probability_score`, `pinball_quantile_loss`, `jeffreys_divergence`, `welford_online_variance`, `wasserstein_policy_optimization`.
- Re-merged (still absent from `main`): full W31-W42 emerging set from `qk_norm` through `information_bottleneck`, with Mel requiring STFT; GAE requiring TD+Advantage; Langevin requiring score matching; front-door requiring back-door; PPO clip requiring Advantage + log-derivative; group-relative advantage requiring Advantage; DPO requiring Bradley-Terry + CE/KL; HMC requiring MH + Langevin; Hopfield requiring Softmax; RSSM requiring ELBO + reparameterization; mediation requiring back-door; f-divergence requiring CE/KL; entropy-regularized RL requiring log-derivative + Bellman; Mirror Descent requiring Bregman; Best-of-N KL requiring CE/KL + rejection sampling; SNIPS requiring IPW; Schrödinger bridge requiring score matching + Sinkhorn; spectral clustering requiring Graph Laplacian; online softmax requiring Softmax Jacobian; Information Bottleneck requiring CE/KL; KTO requiring CE/KL when considered.
- Existing topics skipped (no renames, deletions, or manual status edits): all foundation entries `01`-`15`.
- `foundation_curriculum.json` and `interest_domains` untouched.
- Domains explored: Transformers, Vision, Representation Learning, Diffusion, RL / Alignment, Recommendation / Bandits, Audio, World Models / SSM memory, Graph ML, Quantitative Finance / Forecasting, Causal Inference, Monte Carlo, Preference Learning, Optimization geometry.
- Sources unavailable: X/Twitter (Tier 5) unused (optional). OpenAI / Anthropic / DeepMind public surfaces were mostly product, interpretability, eval, or agent-demo posts; reusable mechanisms retained include Best-of-N KL, online softmax, CRPS (forecasting / GenCast-adjacent), and WPO (ICML 2025). Prior weekly draft PRs (W31-W42) remain unmerged on `main`, so emerging topics were revalidated and re-merged.
