# Weekly AI Math Digest

Generated: 2026-11-01 (ISO 2026-W44)

---

# Suggested Next Module

## Softmax Jacobian & Backpropagation (`softmax_jacobian`)

Overall Score: **39 / 40**

Reason:

Only `attention_scaling` has three-layer evidence. Softmax Jacobian is still the live hinge on the transformer spine: Multi-Head Attention, causal masks, online softmax, and FlashAttention all depend on it. LayerNorm and Adam can match the raw score, but Softmax uniquely continues the only completed module and unlocks the largest set of foundation successors this week. If the author builds only one module, this is unquestionably the highest long-term value choice.

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
| Domain coverage | Shipped: Transformer Core only. Backlog seeds now also cover critic-free RL (RLOO/TRPO), correct KL gradients, AIPW, JS divergence, Fisher geometry, IWAE, and sliced Wasserstein beside prior W31-W43 domains |
| Curriculum continuity | Broken after Module 01 until Softmax Jacobian ships |
| Prerequisite graph | Softmax is the critical cut vertex before MHA, masks, KV, online softmax, Flash, and Hopfield |
| Implementation backlog | 14 foundation + 90 emerging topics with `github: todo` |
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
| 3 | Adam from First Principles (`adam_optimizer`) | 39 | Interview staple; no hard prereq | Weight decay, schedules, later Muon / AdaFisher |
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
5. **ELBO + reparameterization** before deep DDPM / VAE / RSSM / IWAE work (emerging seeds exist; not shipped)
6. **Score matching + Langevin** beside DDPM / flow matching / Schrödinger bridge
7. **Log-derivative + Bellman + TD / Advantage** before REINFORCE / RLOO / PPO / GRPO / TRPO / DPG / RWR
8. **Bradley-Terry before DPO**; **CE/KL before KTO / f-divergence / Best-of-N KL / Jeffreys / JS**
9. **Bregman divergence before Mirror Descent** (seeded as a linked pair)
10. **Fisher Information before deep Natural Gradient / AdaFisher stories** (Fisher seeded this week)
11. **Natural Gradient + Wasserstein + Advantage before WPO**
12. **Itô's Lemma** before first-principles Black-Scholes depth
13. **IPW before SNIPS / AIPW** (AIPW now seeded on IPW)
14. **STFT before Mel filterbank**
15. **Graph Laplacian before spectral clustering**
16. **Wasserstein before sliced Wasserstein / Schrödinger-bridge-only OT treatments**
17. **HiPPO before S4 / Elastic Memory / long-context SSM variants**
18. **Momentum SGD before Nesterov** (Nesterov already seeded as the lookahead variant)

---

# Emerging Candidates

Accepted after `scoring.md` hard gates. Prior W31-W43 emerging set revalidated and re-merged (still absent from `main`). New W44 accepts below.

| Topic | Domain | Score | Confidence | Why Interesting | Blocked On |
|--------|--------|------:|------------|-----------------|------------|
| reinforce_leave_one_out | Reinforcement Learning | 37 | High | Unbiased LOO baseline $A_i=K/(K-1)(R_i-\bar R)$; critic-free hinge beside GRPO | Log-derivative |
| kl_regularization_gradient | Reinforcement Learning | 36 | High | Score-function + pathwise KL gradient; Meta 2025 autodiff-through-MC-KL pitfall | CE/KL + log-derivative |
| augmented_inverse_propensity | Causal Inference | 36 | High | Doubly robust AIPW; outcome model + IPW residual; Neyman orthogonality sketch | IPW |
| jensen_shannon_divergence | Loss / Representation | 35 | High | Symmetric bounded mixture-of-KLs; $\sqrt{\mathrm{JS}}$ metric; GAN / attention-policy staple | CE/KL |
| fisher_information | Optimization | 35 | High | $F=\mathbb{E}[ss^\top]=-\mathbb{E}[\nabla^2\log p]$; geometry behind natural gradient | - |
| importance_weighted_elbo | Diffusion / Generative | 35 | High | Multi-sample $\log(\mathrm{avg}\,w_i)$ tighter than ELBO; IWAE identity | ELBO + importance sampling |
| sliced_wasserstein | Diffusion / Generative | 34 | High | Average closed-form 1-D Wasserstein over projections; SWAE hinge | Wasserstein |
| trust_region_policy_optimization | Reinforcement Learning | 34 | High | KL-ball constrained policy step; PPO's mathematical ancestor (Meta GRAPE path) | Advantage + CE/KL |

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
| Muon / Newton-Schulz / AdaFisher optimizer variants | Adam (+ Fisher / Natural Gradient for AdaFisher) |
| Norm×Direction linear attention / Monarch / CEDAR / ARM / MARCH / Slim Attention / attention sinks | MHA (+ KV where memory-bound) |
| Kernel / linear attention (Performer FAVOR+) | Multi-Head Attention (+ Softmax) |
| Multi-token / differential / gated / hierarchical / verified sparse attention (vAttention) | Multi-Head Attention (+ Softmax) |
| Sigmoid self-attention / α-entmax / AdaSplash sparse attention | Softmax Jacobian (+ MHA) |
| BalanceKV / streaming attention approximation via discrepancy theory | Multi-Head Attention + KV Cache |
| Consistency models / CFG / DDIM | DDPM forward process |
| Rectified flow / OT-CFM / Contrastive FM / Source-guided FM / Topological FM / Bures-Wasserstein FM / Semidiscrete OT-FM / high-order flow matching | Flow matching (+ Wasserstein / Sinkhorn / Graph Laplacian where claimed) |
| DiffusionNFT / Flow Policy Gradients / ReinFlow / discrete diffusion policy stacks | Flow matching + Advantage / log-derivative (+ DDPM where reverse-process bound) |
| Moment Matching Distillation / RMMD stacks | DDPM (+ score matching / MMD) |
| Counterfactual dynamic OT maps | Back-door + flow matching + Wasserstein |
| GAT / Graph Attention | Message passing (+ Softmax/MHA intuition) |
| Particle filter / RTS smoother / SMC / EKF | Kalman filter |
| Black-Scholes Greeks | Black-Scholes PDE + Itô |
| Speculative decoding (as emerging) | Already foundation `f35`; also needs sampling + KV |
| SIGReg / Causal-JEPA | JEPA predictive objective |
| Scalable-Softmax / length-aware softmax / ZeroS | Softmax Jacobian (+ MHA for ZeroS) |
| GraphAE / representation-aware advantage estimators | Advantage + message passing |
| GSPO / DAPO / CISPO / Dr. GRPO objective tweaks | Advantage + PPO clip / group-relative advantage |
| Reinforced Attention Learning / attention-as-policy composites | MHA + Softmax + Advantage |
| SANTA++ / representative-key attention sampling | MHA + KV Cache + importance sampling |
| Sparse-plus-low-rank quasi-Newton Sinkhorn solvers | Sinkhorn (+ conjugate gradient / Newton tooling) |

---

# Rejected This Week

| Topic | Reason |
|--------|--------|
| Limitations-of-softmax / Normalization-in-Attention-Dynamics / Lightning Self-Attention geometry papers | Diagnostic or algebraic analysis of existing attention, not a new reusable implementable mechanism |
| Attention-as-one-sided Entropic OT reframing | Re-derives scaled-dot-product attention; overlaps Softmax + Sinkhorn seeds without a distinct module |
| AlphaEvolve / coding-agent product posts | Product/agent systems, not a mathematical mechanism |
| HybridNorm / Peri-LN as emerging merges | Prerequisite gate: need LayerNorm + residuals first (listed under Blocked) |
| BatchNorm / RMSNorm / temperature / log-sum-exp as emerging | Already in `foundation_curriculum.json` (`f04`, `f05`, `f14`, `f15`); novelty gate |
| AdaLayerNorm as emerging | Thin FiLM + LayerNorm variant; FiLM already seeded |
| DiffusionNFT / ReinFlow / FPO composite stacks as standalone merges | Composite diffusion×RL systems; extractable hinges already covered or blocked on flow matching |
| Continuous batching / SpecJAX serving posts | Systems scheduling / library launches, not first-principles math modules |
| QLoRA / NF4 quantization stacks | Prerequisite gate on LoRA; also hardware/numerics-heavy vs mechanism clarity |
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
| Optimization | Queued: Adam, Weight Decay. Emerging: Momentum, Nesterov, EMA, Natural Gradient, Fisher Information, Polyak, Hutchinson, Bregman, Mirror Descent, Conjugate Gradient |
| Loss Functions | Queued: CE/KL, Focal, InfoNCE. Emerging: CTC, BPR, Hinge, Pinball, VICReg/Barlow/BYOL, MMD, f-divergence, Jeffreys, Jensen-Shannon |
| Diffusion | Queued: DDPM. Emerging: Score matching, Flow matching, Langevin, ELBO, reparameterization, IWAE, Schrödinger bridge, Sliced Wasserstein |
| Reinforcement Learning | Emerging: log-derivative, Bellman, TD, Advantage, GAE, group advantage, RLOO, PPO clip, TRPO, KL regularization gradient, DPG, RWR, WPO, entropy-regularized RL, DPO path, Best-of-N KL |
| Computer Vision | Emerging: ViT patch embedding, spectral norm, Fourier features, FiLM |
| Representation Learning | Emerging: VICReg, Barlow, BYOL, JEPA, sparse dictionary, CCA, MMD, Information Bottleneck, Jensen-Shannon |
| Recommendation Systems | Emerging: Two-tower, BPR, ALS, Thompson Sampling, UCB |
| World Models | Emerging: JEPA, RSSM variational bound, HiPPO polynomial projection, Schrödinger bridge |
| Audio / Speech | Emerging: STFT → Mel, CTC |
| Graph ML | Emerging: Message passing, Graph Laplacian, Spectral Clustering |
| Quantitative Finance | Emerging: Black-Scholes PDE, Itô lemma, CRPS, Pinball quantile loss |
| Causal Inference | Emerging: IPW, SNIPS, AIPW, back-door, front-door, mediation effects |
| Monte Carlo / Uncertainty | Emerging: MH, importance sampling, rejection sampling, HMC, control variates, conformal prediction, Welford online variance |
| Preference Learning | Emerging: Bradley-Terry, DPO, Kahneman-Tversky Optimization, Best-of-N KL, Jeffreys divergence |

---

# Notes

- Suggested next module remains **Softmax Jacobian** (same objective ranking as W32-W43) because Module 01 is still the only shipped artifact and Softmax is still the continuity cut vertex.
- New topics merged into `topics.json` this week: `reinforce_leave_one_out`, `kl_regularization_gradient`, `augmented_inverse_propensity`, `jensen_shannon_divergence`, `fisher_information`, `importance_weighted_elbo`, `sliced_wasserstein`, `trust_region_policy_optimization`.
- Re-merged (still absent from `main`): full W31-W43 emerging set from `qk_norm` through `wasserstein_policy_optimization`, with Mel requiring STFT; GAE requiring TD+Advantage; Langevin requiring score matching; front-door requiring back-door; PPO clip requiring Advantage + log-derivative; group-relative advantage requiring Advantage; DPO requiring Bradley-Terry + CE/KL; HMC requiring MH + Langevin; Hopfield requiring Softmax; RSSM requiring ELBO + reparameterization; mediation requiring back-door; f-divergence requiring CE/KL; entropy-regularized RL requiring log-derivative + Bellman; Mirror Descent requiring Bregman; Best-of-N KL requiring CE/KL + rejection sampling; SNIPS requiring IPW; Schrödinger bridge requiring score matching + Sinkhorn; spectral clustering requiring Graph Laplacian; online softmax requiring Softmax Jacobian; Information Bottleneck requiring CE/KL; KTO requiring CE/KL when considered; DPG requiring Advantage; RWR requiring log-derivative; Jeffreys requiring CE/KL; WPO requiring Wasserstein + Natural Gradient + Advantage; RLOO requiring log-derivative; KL regularization gradient requiring CE/KL + log-derivative; AIPW requiring IPW; JS requiring CE/KL; IWAE requiring ELBO + importance sampling; sliced Wasserstein requiring Wasserstein; TRPO requiring Advantage + CE/KL.
- Existing topics skipped (no renames, deletions, or manual status edits): all foundation entries `01`-`15`.
- `foundation_curriculum.json` and `interest_domains` untouched.
- Domains explored: Transformers, Vision, Representation Learning, Diffusion, RL / Alignment, Recommendation / Bandits, Audio, World Models / SSM memory, Graph ML, Quantitative Finance / Forecasting, Causal Inference, Monte Carlo, Preference Learning, Optimization geometry.
- Sources unavailable: X/Twitter (Tier 5) unused (optional). OpenAI / Anthropic / DeepMind public surfaces were mostly product, interpretability, eval, agent-demo, or AlphaEvolve posts; reusable mechanisms retained include Meta KL-gradient / GRAPE RL path (RLOO, TRPO), online softmax (HF), AIPW (causal), Fisher / JS / IWAE / sliced Wasserstein (venue + classic mechanism literature). Prior weekly draft PRs (W31-W43) remain unmerged on `main`, so emerging topics were revalidated and re-merged.
