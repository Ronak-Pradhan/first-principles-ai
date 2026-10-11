# Weekly AI Math Digest

Generated: 2026-10-11 (ISO 2026-W41)

---

# Suggested Next Module

## Softmax Jacobian & Backpropagation (`softmax_jacobian`)

Overall Score: **39 / 40**

Reason:

Only `attention_scaling` has three-layer evidence. Softmax Jacobian is the live hinge on the transformer spine: Multi-Head Attention, causal masks, and FlashAttention all depend on it. LayerNorm and Adam can match the raw score, but Softmax uniquely continues the only completed module and unlocks the largest set of foundation successors this week. If the author builds only one module, this is unquestionably the highest long-term value choice.

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
| Domain coverage | Shipped: Transformer Core only. Backlog seeds now span preference learning, bandits/RecSys, SSM memory, optimization geometry, and prior W31-W40 domains |
| Curriculum continuity | Broken after Module 01 until Softmax Jacobian ships |
| Prerequisite graph | Softmax is the critical cut vertex before MHA, masks, KV, Flash, and Hopfield |
| Implementation backlog | 14 foundation + 64 emerging topics with `github: todo` |
| Blog backlog | `attention_scaling` blog still `wip`; all other blogs `todo` |
| Research backlog | All non-01 research statuses remain `todo` |

**Single largest curriculum weakness:** Softmax Jacobian is missing, so the transformer spine cannot advance and continuity from the only shipped module is stalled.

**Underrepresented ML domains (no shipped modules):** Vision, Representation Learning, Diffusion, RL, Recommendation, Audio, World Models, Graph ML, Quantitative Finance, Causal Inference.

---

# Foundation Gaps

Remaining foundation topics evaluated with `scoring.md`. Softmax preferred for continuity even when LayerNorm/Adam tie on raw score.

| Rank | Topic | Score | Why Now | Unlocks |
|------|------:|--------|----------|----------|
| 1 | Softmax Jacobian (`softmax_jacobian`) | 39 | Continues Module 01; prereq satisfied | MHA, masks, Flash path, Hopfield |
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
4. **ELBO + reparameterization** before deep DDPM / VAE / RSSM work (emerging seeds exist; not shipped)
5. **Score matching + Langevin** beside DDPM / flow matching
6. **Log-derivative + Bellman + TD / Advantage** before REINFORCE / PPO / GRPO (emerging seeds exist)
7. **Bradley-Terry before DPO**; **CE/KL before KTO / f-divergence** (preference path seeded)
8. **Bregman divergence before Mirror Descent** (merged this week as a linked pair)
9. **Itô's Lemma** before first-principles Black-Scholes depth
10. **STFT before Mel filterbank**
11. **Graph Laplacian beside message passing**
12. **Wasserstein before Sinkhorn-only OT treatments**
13. **HiPPO before S4 / Elastic Memory / long-context SSM variants**

---

# Emerging Candidates

Accepted after `scoring.md` hard gates. Prior W31-W40 emerging set revalidated and re-merged (still absent from `main`). New W41 accepts below.

| Topic | Domain | Score | Confidence | Why Interesting | Blocked On |
|--------|--------|------:|------------|-----------------|------------|
| thompson_sampling | Recommendation / Bandits | 37 | High | Posterior-sample-then-greedy explore-exploit; RecSys cold-start interview staple | - |
| hippo_polynomial_projection | World Models / Sequence | 36 | High | Closed-form online polynomial memory ODE; unlocks SSM / S4 lineage | - |
| ucb_confidence_bound | Recommendation / Bandits | 35 | High | Optimistic μ̂ + bonus rule; frequentist counterpart to Thompson | - |
| mirror_descent | Optimization | 34 | High | Bregman proximal updates; recovers projected GD and Hedge | bregman_divergence |
| bregman_divergence | Optimization | 33 | High | Geometry of KL / Euclidean / entropic distances | - |
| kahneman_tversky_optimization | Preference Learning | 33 | High | Prospect utility on binary labels; HALO without paired preferences | CE vs KL |

---

# Blocked Candidates

Worth revisiting after prerequisites. **Not merged** into `topics.json`.

| Topic | Waiting For |
|--------|-------------|
| Peri-LN / HybridNorm / SpanNorm / SimpleNorm / SiameseNorm / DeepNorm | LayerNorm + residual connections |
| MoE routers (ProbMoE / STAR / AAR / load-balance variants) | MoE routing foundation (`f34`) |
| GQA / MQA | Multi-Head Attention + KV Cache |
| FlashAttention v2 / v3 | FlashAttention |
| YaRN / ClockRoPE / RoPE variants | RoPE |
| QLoRA / LoRA+ / DoRA | LoRA |
| Muon / Newton-Schulz optimizer variants | Adam |
| Norm×Direction linear attention / Monarch / CEDAR / ARM / MARCH / Slim Attention / attention sinks | MHA (+ KV where memory-bound) |
| Multi-token / differential / gated / hierarchical attention | Multi-Head Attention |
| Consistency models / CFG / DDIM | DDPM forward process |
| Rectified flow / OT-CFM / Contrastive FM / Source-guided FM / Topological FM / Bures-Wasserstein FM / Semidiscrete OT-FM | Flow matching (+ Wasserstein / Sinkhorn / Graph Laplacian where claimed) |
| Counterfactual dynamic OT maps | Back-door + flow matching + Wasserstein |
| AIPW / Neyman orthogonal scores | Inverse propensity weighting |
| GAT / Graph Attention | Message passing (+ Softmax/MHA intuition) |
| Particle filter / RTS smoother / SMC decoding particles | Kalman filter |
| Black-Scholes Greeks | Black-Scholes PDE + Itô |
| Speculative decoding (as emerging) | Already foundation `f35`; also needs sampling + KV |
| SIGReg / Causal-JEPA | JEPA predictive objective |
| Scalable-Softmax / length-aware softmax normalizers | Softmax Jacobian |
| ZeroS / zero-sum linear attention | Softmax + MHA (+ LN for stability claims) |
| GraphAE / representation-aware advantage estimators | Advantage + message passing |
| GSPO / DAPO / CISPO / Dr. GRPO objective tweaks | Advantage + PPO clip / group-relative advantage |
| SANTA++ / representative-key attention sampling | MHA + KV Cache + importance sampling |

---

# Rejected This Week

| Topic | Reason |
|--------|--------|
| Titans / MIRAS product framing as a module | Lab blog is useful for mechanism hunting, but the packaged architecture fails evergreen/portfolio gates vs HiPPO; surprise-gated associative update scored ~28 |
| Memory Layers sparse KV lookup | Engineering-heavy sparse memory table; score <30 for standalone first-principles module |
| BEACON / OptScale adaptive Best-of-N | Inference product / stopping heuristics; not a reusable derivation-first mechanism |
| Decoding-as-simplex KKT unification | Overlaps foundation Top-k/Top-p (`f36`); meta-framework rather than one implementable identity |
| Identity Preference Optimization (IPO) | Thin DPO regularization variant; prefer Bradley-Terry → DPO → KTO path |
| Inverse scaling in test-time compute (Anthropic) | Evaluation / failure-mode study, not a mathematical mechanism |
| Inkling / model architecture comparison posts | Model release notes and architecture tourism |
| Nested Learning / I-CON / Adjoint Sampling stacks | Composite paradigms; fail clean standalone derivation + small PyTorch module fit |
| RouteLLM / LLM routers | Product-style routing systems |
| FlashPairformer / Triton kernels | Hardware kernels, not math modules |
| gpt-oss / model release writeups | Product / checkpoint announcements |
| Prompt / Declarative Attention protocols | Prompt engineering |
| InfoNCE aliases / CLIP rebrands | Duplicate of foundation `info_nce` |
| Sparsemax / Entmax / Soft-DTW / STE alone | Score <30 or weak portfolio vs Softmax Jacobian |
| Reward hacking survey framing | Pedagogy / taxonomy post without a single implementable mechanism |

---

# Repository Coverage

| Area | Coverage |
|------|----------|
| Transformer Core | Shipped: Attention Scaling. Queued: Softmax, LN, MHA. Emerging: QK-Norm, Hopfield |
| Optimization | Queued: Adam, Weight Decay. Emerging: Natural Gradient, Polyak EMA, Hutchinson, Bregman, Mirror Descent |
| Loss Functions | Queued: CE/KL, Focal, InfoNCE. Emerging: CTC, BPR, VICReg/Barlow/BYOL, MMD, f-divergence |
| Diffusion | Queued: DDPM. Emerging: Score matching, Flow matching, Langevin, ELBO, reparameterization |
| Reinforcement Learning | Emerging: log-derivative, Bellman, TD, Advantage, GAE, group advantage, PPO clip, entropy-regularized RL, DPO / KTO path |
| Computer Vision | Emerging: ViT patch embedding, spectral norm, Fourier features, FiLM |
| Representation Learning | Emerging: VICReg, Barlow, BYOL, JEPA, sparse dictionary, CCA, MMD |
| Recommendation Systems | Emerging: Two-tower, BPR, ALS, Thompson Sampling, UCB |
| World Models | Emerging: JEPA, RSSM variational bound, HiPPO polynomial projection |
| Audio / Speech | Emerging: STFT → Mel, CTC |
| Graph ML | Emerging: Message passing, Graph Laplacian |
| Quantitative Finance | Emerging: Black-Scholes PDE, Itô lemma |
| Causal Inference | Emerging: IPW, back-door, front-door, mediation effects |
| Monte Carlo / Uncertainty | Emerging: MH, importance sampling, rejection sampling, HMC, control variates, conformal prediction |
| Preference Learning | Emerging: Bradley-Terry, DPO, Kahneman-Tversky Optimization |

---

# Notes

- Suggested next module remains **Softmax Jacobian** (same objective ranking as W32-W40) because Module 01 is still the only shipped artifact and Softmax is still the continuity cut vertex.
- New topics merged into `topics.json` this week: `thompson_sampling`, `ucb_confidence_bound`, `hippo_polynomial_projection`, `bregman_divergence`, `mirror_descent`, `kahneman_tversky_optimization`.
- Re-merged (still absent from `main`): full W31-W40 emerging set from `qk_norm` through `canonical_correlation_analysis`, with Mel requiring STFT; GAE requiring TD+Advantage; Langevin requiring score matching; front-door requiring back-door; PPO clip requiring Advantage + log-derivative; group-relative advantage requiring Advantage; DPO requiring Bradley-Terry + CE/KL; HMC requiring MH + Langevin; Hopfield requiring Softmax; RSSM requiring ELBO + reparameterization; mediation requiring back-door; f-divergence requiring CE/KL; entropy-regularized RL requiring log-derivative + Bellman; KTO requiring CE/KL; Mirror Descent requiring Bregman.
- Existing topics skipped (no renames, deletions, or manual status edits): all foundation entries `01`-`15`.
- `foundation_curriculum.json` and `interest_domains` untouched.
- Domains explored: Transformers, Vision, Representation Learning, Diffusion, RL, Recommendation / Bandits, Audio, World Models / SSM memory, Graph ML, Quantitative Finance, Causal Inference, Monte Carlo, Preference Learning, Optimization geometry.
- Sources unavailable: X/Twitter (Tier 5) unused (optional). OpenAI / Anthropic / DeepMind public surfaces were mostly product, interpretability, eval, or agent-demo posts; Google Research Titans/MIRAS retained only as a pointer to memory mechanisms (HiPPO preferred). Prior weekly draft PRs (W31-W40) remain unmerged on `main`, so emerging topics were revalidated and re-merged.
