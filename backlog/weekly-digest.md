# Weekly AI Math Digest

Generated: 2026-11-08 (ISO 2026-W45)

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
| Domain coverage | Shipped: Transformer Core only. Backlog seeds now also cover Personalized PageRank, Adaptive Computation Time, Nadaraya-Watson kernels, K-FAC, Gaussian processes, and Hessian-vector products beside prior W31-W44 domains |
| Curriculum continuity | Broken after Module 01 until Softmax Jacobian ships |
| Prerequisite graph | Softmax is the critical cut vertex before MHA, masks, KV, online softmax, Flash, and Hopfield |
| Implementation backlog | 14 foundation + 96 emerging topics with `github: todo` |
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
| 3 | Adam from First Principles (`adam_optimizer`) | 39 | Interview staple; no hard prereq | Weight decay, schedules, later Muon / K-FAC / AdaFisher |
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
10. **Fisher Information + Natural Gradient before K-FAC / AdaFisher depth** (K-FAC seeded this week on that pair + Adam)
11. **Natural Gradient + Wasserstein + Advantage before WPO**
12. **Itô's Lemma** before first-principles Black-Scholes depth
13. **IPW before SNIPS / AIPW**
14. **STFT before Mel filterbank**
15. **Graph Laplacian before spectral clustering**; **Personalized PageRank** now seeds the random-walk recsys bridge beside message passing
16. **Wasserstein before sliced Wasserstein / Schrödinger-bridge-only OT treatments**
17. **HiPPO before S4 / Elastic Memory / long-context SSM variants**
18. **Momentum SGD before Nesterov** (Nesterov already seeded as the lookahead variant)
19. **Adaptive Computation Time** before Universal-Transformer / recurrent-depth / early-exit products

---

# Emerging Candidates

Accepted after `scoring.md` hard gates. Prior W31-W44 emerging set revalidated and re-merged (still absent from `main`). New W45 accepts below.

| Topic | Domain | Score | Confidence | Why Interesting | Blocked On |
|--------|--------|------:|------------|-----------------|------------|
| personalized_pagerank | Graph ML / RecSys | 37 | High | Teleport-biased stationary walk π=αs+(1-α)πP; bipartite retrieval hinge surfaced by RankGraph-style systems without the product stack | - |
| adaptive_computation_time | Adaptive Compute | 36 | High | Halting probs + remainder mass + ponder cost; test-time compute math from Graves, revived in Lilian Weng thinking notes | - |
| nadaraya_watson_kernel | Representation Learning | 36 | High | Classic kernel smoother; attention-as-kernel / ICLR 2026 KERN router substrate without MoE packaging | - |
| kronecker_factored_fisher | Optimization | 35 | High | K-FAC A⊗G Fisher blocks; makes SOAP/Shampoo readable later without shipping those optimizers yet | Adam + Natural Gradient + Fisher |
| gaussian_process_regression | Probabilistic Models | 34 | High | Posterior mean/variance via Gram + Cholesky; Bayesian nonparametric hinge for kernels / SDE inference later | - |
| hessian_vector_product | Optimization | 33 | High | Pearlmutter Hv without forming H; CG-Newton / second-order interview staple | - |

---

# Blocked Candidates

Topics worth revisiting after prerequisite modules are complete. Not merged into `topics.json`.

| Topic | Waiting For |
|--------|-------------|
| FlashAttention v2 / v3 | FlashAttention |
| YaRN / ClockRoPE / other RoPE variants | RoPE |
| GQA / MQA / MLA / KV-sharing | Multi-Head Attention + KV Cache |
| QLoRA / LoRA+ / DoRA | LoRA |
| Muon / Newton-Schulz / MuonClip / QK-Clip | Adam (+ MHA for QK-Clip) |
| SOAP / Shampoo-as-optimizer packaging | Adam + Kronecker / Natural Gradient path |
| AdaFisher | Adam + Fisher Information |
| Peri-LN / HybridNorm / DeepNorm / SpanNorm / SimpleNorm / SiameseNorm / Mix-LN / nGPT | LayerNorm + Residual connections |
| MoE routers / KERN / perturbed cosine router | Mixture-of-Experts foundation (`f34`) |
| Norm×Direction / Monarch / CEDAR / ARM / MARCH / Slim Attention / attention sinks | Multi-Head Attention (+ KV where relevant) |
| Performer FAVOR+ / linear attention | Multi-Head Attention + Softmax |
| Multi-token prediction / vAttention verified sparse attention | Multi-Head Attention (+ KV / Softmax) |
| Sigmoid self-attention / α-entmax / AdaSplash / Sparsemax-as-default | Softmax (+ MHA for attention swaps) |
| BalanceKV | Multi-Head Attention + KV Cache |
| QUEST / spherical attention | Softmax + Multi-Head Attention |
| Consistency models / CFG / DDIM | DDPM |
| Flow-matching OT variants (OT-CFM, rectified flow stacks, Source-guided / Topological / Bures-Wasserstein / Semidiscrete OT-FM) | Flow Matching (+ OT prereqs as listed) |
| DiffusionNFT / Flow Policy Gradients / ReinFlow | Flow Matching + Advantage / log-derivative |
| Moment Matching Distillation | DDPM (+ score / MMD) |
| GAT | Message Passing |
| Particle filter / RTS / SMC / EKF | Kalman Filter |
| Black-Scholes Greeks | Black-Scholes PDE (+ Itô) |
| Speculative decoding / multi-draft OT speculative sampling | Speculative decoding foundation (`f35`) + sampling |
| ZeroS / Scalable-Softmax | Softmax (+ MHA) |
| GraphAE | Advantage + Message Passing |
| GSPO / DAPO / CISPO | PPO / GRPO path |
| Reinforced Attention composites | MHA + Softmax + Advantage |
| SANTA++ | MHA + KV + Importance Sampling |
| FlashSinkhorn / cuRegOT sparse+low-rank Sinkhorn solvers | Sinkhorn (systems/hardware packaging rejected; math already seeded) |
| SING latent-SDE natural-gradient stack | Natural Gradient + GP / SDE path |
| HollowFlow / NoBGNN likelihood stacks | Message Passing + Flow Matching |

---

# Rejected This Week

Topics considered but intentionally rejected.

| Topic | Reason |
|--------|--------|
| LASER recursive safety sampling (OpenAI) | Eval / data-curation pipeline, not a reusable mathematical mechanism |
| Anthropic Hot Mess bias-variance misalignment study | Evaluation framing, not an implementable first-principles module |
| AlphaEvolve / product research agents | Product / search agent, not a timeless mechanism |
| Raschka GQA / MLA / SWA architecture tourism | Prerequisite-blocked attention variants; no new mechanism beyond existing blocks |
| Advantage-weighted supervised finetuning (Netflix A-SFT) | Thin alias of seeded `reward_weighted_regression` |
| GeoCF / RankGraph-2 / CaGE / CausalDiffRec composites | System or explainer stacks; extractable PPR / IPW / diffusion pieces already covered or seeded |
| Softmax/normalization limitation and Lightning Self-Attention geometry papers | Diagnostics without a new implementable mechanism |
| Attention-as-EOT reframes | Restate Softmax + Sinkhorn without a distinct module |
| BatchNorm / RMSNorm / temperature / logsumexp as emerging | Foundation curriculum overlap (`f04`/`f05`/`f14`/`f15`) |
| AdaLayerNorm | Thin FiLM + LayerNorm variant |
| IPO | Thin DPO variant |
| InfoNCE aliases / Sparsemax / Entmax / Soft-DTW / STE | Alias, blocked, or previously scored <30 |
| Continuous batching / SpecJAX / serving posts | Systems packaging, not first-principles math |
| Hardware kernels (FlashPairformer, IO-only Sinkhorn speedups) | Hardware optimization, fails authenticity / evergreen portfolio fit |
| Prompt engineering / declarative attention protocols | Rejected by discovery policy |
| Model releases, datasets, benchmarks, APIs | Rejected by discovery policy |
| Scaling-laws-only / reward-hacking survey posts | No standalone derivation module |

---

# Repository Coverage

| Area | Coverage |
|------|----------|
| Transformer Core | Shipped: Attention Scaling. Queued: Softmax, LN, MHA, RoPE, masks (curriculum). Emerging: QK-Norm, Online Softmax, Hopfield |
| Optimization | Queued: Adam, Weight Decay. Emerging: Momentum, Nesterov, EMA, Polyak, CG, Natural Gradient, Fisher, K-FAC, Hessian-vector products, Bregman, Mirror Descent, Welford |
| Loss Functions | Queued: CE/KL, Focal, InfoNCE. Emerging: Hinge, pinball, CRPS, JS, Jeffreys, f-divergence, Best-of-N KL, IB, KTO path |
| Diffusion | Queued: DDPM. Emerging: Score matching, Flow matching, ELBO, IWAE, Langevin, Sinkhorn, Wasserstein, sliced Wasserstein, Schrödinger bridge |
| Reinforcement Learning | Emerging: Log-derivative, Bellman, TD, Advantage, GAE, RLOO, TRPO, PPO clip, GRPO-style group-relative advantage, DPG, RWR, WPO, entropy-regularized RL, KL regularization gradient |
| Computer Vision | Emerging: ViT patch embedding, Fourier features, FiLM |
| Representation Learning | Emerging: VICReg, Barlow, BYOL, JEPA, MMD, sparse dictionary, Nadaraya-Watson, CCA |
| Recommendation Systems | Emerging: Two-tower, BPR, ALS, Thompson Sampling, UCB, Personalized PageRank |
| World Models | Emerging: JEPA, RSSM variational bound, HiPPO |
| Audio / Speech | Emerging: STFT → Mel, CTC |
| Graph ML | Emerging: Message passing, Graph Laplacian, Spectral clustering, Personalized PageRank |
| Quantitative Finance | Emerging: Black-Scholes PDE, Itô, CRPS, pinball |
| Causal Inference | Emerging: IPW, SNIPS, AIPW, back-door, front-door, mediation |
| Adaptive Compute / Probabilistic | Emerging: Adaptive Computation Time, Gaussian Process Regression, Gumbel-Softmax, conformal prediction, Kalman |
| Preference Learning | Emerging: Bradley-Terry, DPO (on CE/KL), rejection sampling |

---

# Notes

- New topics merged into `topics.json` (W45): `personalized_pagerank`, `adaptive_computation_time`, `nadaraya_watson_kernel`, `kronecker_factored_fisher`, `gaussian_process_regression`, `hessian_vector_product`.
- Revalidated and re-merged W31-W44 emerging set (`qk_norm` through `trust_region_policy_optimization`) because those merges still had not landed on `main`.
- Existing manual foundation topics were left untouched (no renames, deletes, or status edits). `foundation_curriculum.json` and `interest_domains` untouched.
- Objective ranking still puts Softmax / LayerNorm / Adam in a near-tie at 39; decision gate selects Softmax for curriculum continuity from the only shipped module.
- Sources unavailable: none for Tier 1-3 this week. Tier 5 (X/Twitter) was optional and unused. OpenAI / Anthropic / DeepMind public surfaces were mostly product, eval, or agent posts; no new mergeable mechanisms extracted there beyond confirming Adaptive Computation Time via Lilian Weng's thinking survey.
