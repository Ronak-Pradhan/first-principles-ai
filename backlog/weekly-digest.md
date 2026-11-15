# Weekly AI Math Digest

Generated: 2026-11-15 (ISO 2026-W46)

---

# Suggested Next Module

## Softmax Jacobian & Backpropagation (`softmax_jacobian`)

Overall Score: **39 / 40**

Reason:

Only `attention_scaling` has three-layer evidence under `modules/`. Softmax Jacobian remains the live hinge on the transformer spine: Multi-Head Attention, causal masks, online softmax, and FlashAttention all depend on it. LayerNorm and Adam can match the raw score, but Softmax uniquely continues the only completed module and unlocks the largest set of foundation successors this week. If the author builds only one module, this is unquestionably the highest long-term value choice.

Prerequisites Satisfied

- ✅ Attention Scaling Factor (`attention_scaling`) shipped under `modules/01_attention_scaling/` (`.md` + `.jpg` + `.ipynb`)
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
| Domain coverage | Shipped: Transformer Core only. Backlog seeds now also cover Influence Functions, Woodbury, TD(λ), 2SLS, Eckart-Young SVD, Jacobian-vector products, and soft-thresholding beside prior W31-W45 domains |
| Curriculum continuity | Broken after Module 01 until Softmax Jacobian ships |
| Prerequisite graph | Softmax is the critical cut vertex before MHA, masks, KV, online softmax, Flash, and Hopfield |
| Implementation backlog | 14 foundation + 103 emerging topics with `github: todo` |
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
7. **Log-derivative + Bellman + TD / Advantage** before REINFORCE / RLOO / PPO / GRPO / TRPO / DPG / RWR; **TD(λ) eligibility** now seeds the multi-step credit bridge after TD
8. **Bradley-Terry before DPO**; **CE/KL before KTO / f-divergence / Best-of-N KL / Jeffreys / JS**
9. **Bregman divergence before Mirror Descent** (seeded as a linked pair)
10. **Fisher Information + Natural Gradient before K-FAC / AdaFisher depth**; **Hessian-vector products before Influence Functions** (both seeded)
11. **Natural Gradient + Wasserstein + Advantage before WPO**
12. **Itô's Lemma** before first-principles Black-Scholes depth
13. **IPW before SNIPS / AIPW**; **2SLS / IV** now seeds unobserved-confounding beside back-door
14. **STFT before Mel filterbank**
15. **Graph Laplacian before spectral clustering**; **Personalized PageRank** seeds the random-walk recsys bridge beside message passing
16. **Wasserstein before sliced Wasserstein / Schrödinger-bridge-only OT treatments**
17. **HiPPO before S4 / Elastic Memory / long-context SSM variants**
18. **Momentum SGD before Nesterov** (Nesterov already seeded as the lookahead variant)
19. **Adaptive Computation Time** before Universal-Transformer / recurrent-depth / early-exit products
20. **Eckart-Young / Woodbury** before treating LoRA rank and low-rank inverse updates as folklore

---

# Emerging Candidates

Accepted after `scoring.md` hard gates. Prior W31-W45 emerging set revalidated and re-merged (still absent from `main`). New W46 accepts below.

| Topic | Domain | Score | Confidence | Why Interesting | Blocked On |
|--------|--------|------:|------------|-----------------|------------|
| influence_functions | Interpretability | 37 | High | Koh-Liang upweighting → −H⁻¹∇L; ICLR 2025 diffusion attribution keeps the mechanism evergreen without shipping diffusion-only packaging | Hessian-vector products |
| woodbury_matrix_identity | Linear Algebra | 36 | High | Rank-k inverse update; LoRA / Kalman / GP online hinge surfaced again by natural-gradient low-rank training notes | - |
| td_lambda_eligibility | Reinforcement Learning | 35 | High | Forward λ-return ↔ backward eligibility recursion; multi-step credit bridge after TD(0) | Temporal Difference Learning |
| two_stage_least_squares | Causal Inference | 34 | High | Classical IV / 2SLS for unobserved confounding; ACM Computing Surveys 2025 and NPIV work keep the mechanism current | - |
| eckart_young_svd | Linear Algebra | 34 | High | Optimal truncated SVD; intrinsic-rank substrate for LoRA / PCA without paper tourism | - |
| jacobian_vector_product | Optimization | 32 | High | Forward-mode Jv companion to seeded Hv products; AD interview staple | - |
| soft_thresholding_proximal | Optimization | 31 | Medium | prox_{λ‖·‖₁} closed form; ISTA hinge beside sparse dictionary learning | - |

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
| Peri-LN / HybridNorm / DeepNorm / SpanNorm / SimpleNorm / SiameseNorm / Mix-LN / nGPT / Peri-LN-from-NeurIPS-2025-normalization-dynamics | LayerNorm + Residual connections |
| MoE routers / KERN / perturbed cosine router | Mixture-of-Experts foundation (`f34`) |
| Norm×Direction / Monarch / CEDAR / ARM / MARCH / Slim Attention / attention sinks | Multi-Head Attention (+ KV where relevant) |
| Performer FAVOR+ / linear attention | Multi-Head Attention + Softmax |
| Multi-token prediction / vAttention verified sparse attention | Multi-Head Attention (+ KV / Softmax) |
| DeepSeek Sparse Attention / learned indexer sparse patterns | Multi-Head Attention + Softmax + KV Cache |
| Sigmoid self-attention / α-entmax / AdaSplash / Sparsemax-as-default | Softmax (+ MHA for attention swaps) |
| BalanceKV | Multi-Head Attention + KV Cache |
| QUEST / spherical attention / S–D routing–filtering attention | Softmax + Multi-Head Attention |
| Contract-and-Broadcast Self-Attention (CBSA) | Multi-Head Attention + Softmax |
| Lattice orthogonal KV-cache compression | Multi-Head Attention + KV Cache |
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
| Titans / MIRAS packaged long-memory modules | HiPPO (+ associative-memory foundations); extractable delta-rule ideas noted but not packaged |

---

# Rejected This Week

Topics considered but intentionally rejected.

| Topic | Reason |
|--------|--------|
| Lilian Weng Scaling Laws, Carefully | Empirical compute-allocation survey; no standalone first-principles derivation module |
| Lilian Weng Harness Engineering for Self-Improvement | Systems / deployment harness, not a reusable mathematical mechanism |
| OpenAI ARGO rubric-matching reward interpretation | Product / search-over-rubrics framing; KL matching already covered by CE/KL path |
| Claude / Anthropic text watermarking (Raschka walkthrough) | Product sampling bias; green-list trick is too thin as a timeless module |
| Raschka October 2026 LLM architecture roundup / GQA / MLA / DSA tourism | Architecture tourism; DSA blocked on MHA+Softmax+KV |
| DeepSeek Sparse Attention as a merge | Prerequisite-blocked sparse attention variant |
| NeurIPS 2025 Normalization-in-Attention-Dynamics Peri-LN recommendation | LN/residual prerequisite gate; scheme comparison not a new mechanism |
| Softmax mean-field / REM toy analyses | Diagnostic theory without a new implementable mechanism beyond Softmax Jacobian |
| Attention-as-EOT / CBSA unrolling reframes | Restate Softmax + Sinkhorn / MHA without a distinct mergeable module |
| Nested Learning / Titans+MIRAS product posts | Paradigm / architecture packaging; HiPPO already the long-memory seed |
| DML-CMR / neural NPIV composites | System stacks; extractable 2SLS mechanism merged instead |
| BatchNorm / RMSNorm / temperature / logsumexp as emerging | Foundation curriculum overlap (`f04`/`f05`/`f14`/`f15`) |
| AdaLayerNorm | Thin FiLM + LayerNorm variant |
| IPO | Thin DPO variant |
| InfoNCE aliases / Sparsemax / Entmax / Soft-DTW / STE | Alias, blocked, or previously scored <30 |
| Neural Tangent Kernel (borderline) | Industry/interview scores too weak after portfolio-fit cut; revisit later |
| Continuous batching / SpecJAX / serving posts | Systems packaging, not first-principles math |
| Hardware kernels (FlashPairformer, IO-only Sinkhorn speedups) | Hardware optimization, fails authenticity / evergreen portfolio fit |
| Prompt engineering / declarative attention protocols | Rejected by discovery policy |
| Model releases, datasets, benchmarks, APIs | Rejected by discovery policy |
| Reward-hacking survey posts without a new identity | No standalone derivation beyond seeded Best-of-N KL / KL regularization |

---

# Repository Coverage

| Area | Coverage |
|------|----------|
| Transformer Core | Shipped: Attention Scaling. Queued: Softmax, LN, MHA, RoPE, masks (curriculum). Emerging: QK-Norm, Online Softmax, Hopfield |
| Optimization | Queued: Adam, Weight Decay. Emerging: Momentum, Nesterov, EMA, Polyak, CG, Natural Gradient, Fisher, K-FAC, Hv/Jv products, Bregman, Mirror Descent, Welford, soft-thresholding, Woodbury |
| Loss Functions | Queued: CE/KL, Focal, InfoNCE. Emerging: Hinge, pinball, CRPS, JS, Jeffreys, f-divergence, Best-of-N KL, IB, KTO path |
| Diffusion | Queued: DDPM. Emerging: Score matching, Flow matching, ELBO, IWAE, Langevin, Sinkhorn, Wasserstein, sliced Wasserstein, Schrödinger bridge |
| Reinforcement Learning | Emerging: Log-derivative, Bellman, TD, Advantage, GAE, TD(λ) eligibility, RLOO, TRPO, PPO clip, GRPO-style group-relative advantage, DPG, RWR, WPO, entropy-regularized RL, KL regularization gradient |
| Computer Vision | Emerging: ViT patch embedding, Fourier features, FiLM |
| Representation Learning | Emerging: VICReg, Barlow, BYOL, JEPA, MMD, sparse dictionary, Nadaraya-Watson, CCA, Eckart-Young |
| Recommendation Systems | Emerging: Two-tower, BPR, ALS, Thompson Sampling, UCB, Personalized PageRank |
| World Models | Emerging: JEPA, RSSM variational bound, HiPPO |
| Audio / Speech | Emerging: STFT → Mel, CTC |
| Graph ML | Emerging: Message passing, Graph Laplacian, Spectral clustering, Personalized PageRank |
| Quantitative Finance | Emerging: Black-Scholes PDE, Itô's Lemma |
| Causal Inference | Emerging: Back-door, Front-door, Mediation, IPW, SNIPS, AIPW, Two-Stage Least Squares |
| Interpretability | Emerging: Influence Functions (on Hv path) |
| Adaptive Compute | Emerging: Adaptive Computation Time |
| Probabilistic Models | Emerging: GP regression, GMM EM |

---

# Notes

- Suggested next module unchanged from W45: Softmax Jacobian remains objectively and editorially first while Module 01 is the only shipped artifact.
- New topics merged into `topics.json`: `influence_functions`, `woodbury_matrix_identity`, `td_lambda_eligibility`, `two_stage_least_squares`, `eckart_young_svd`, `jacobian_vector_product`, `soft_thresholding_proximal`.
- Re-merged (still absent from `main`): prior W31-W45 emerging set (`qk_norm` through `hessian_vector_product`), with Mel requiring STFT; GAE requiring TD+Advantage; Langevin requiring score matching; front-door requiring back-door; PPO clip requiring Advantage + log-derivative; group-relative advantage requiring Advantage; DPO requiring Bradley-Terry + CE/KL; HMC requiring MH + Langevin; Hopfield requiring Softmax; RSSM requiring ELBO + reparameterization; mediation requiring back-door; f-divergence requiring CE/KL; entropy-regularized RL requiring log-derivative + Bellman; Mirror Descent requiring Bregman; Best-of-N KL requiring CE/KL + rejection sampling; SNIPS requiring IPW; Schrödinger bridge requiring score matching + Sinkhorn; spectral clustering requiring Graph Laplacian; online softmax requiring Softmax Jacobian; Information Bottleneck requiring CE/KL; DPG requiring Advantage; RWR requiring log-derivative; Jeffreys requiring CE/KL; WPO requiring Wasserstein + Natural Gradient + Advantage; RLOO requiring log-derivative; KL regularization gradient requiring CE/KL + log-derivative; AIPW requiring IPW; JS requiring CE/KL; IWAE requiring ELBO + importance sampling; sliced Wasserstein requiring Wasserstein; TRPO requiring Advantage + CE/KL; K-FAC requiring Adam + Natural Gradient + Fisher; Influence Functions requiring Hessian-vector products; TD(λ) requiring Temporal Difference Learning.
- Existing topics skipped (no renames, deletes, or manual-status edits): all 15 foundation backlog entries preserved exactly.
- `foundation_curriculum.json` and `interest_domains` were not modified.
- Sources unavailable: X/Twitter (Tier 5) not queried this week; optional by policy.
- Domains explored: Transformers, Optimization, Linear Algebra, RL, Causal Inference, Interpretability, Diffusion-adjacent OT, Graph/RecSys (revalidation), Audio (no new merge), Quant Finance (no new merge), Vision (no new merge beyond prior seeds).
