# Weekly AI Math Digest

Generated: 2026-08-30 (2026-W35)

---

# Suggested Next Module

## Softmax Jacobian & Backpropagation (`softmax_jacobian`)

Overall Score: **39 / 40**

Reason:

Attention Scaling is the only shipped three-layer module. Softmax is the immediate mathematical continuation: the Jacobian `diag(p) - ppᵀ` explains saturation, gradient coupling, and why later kernels (FlashAttention tiling, attention masks, multi-head backprop) behave as they do. No emerging topic beats this on curriculum continuity, interview value, or future unlocks while the transformer spine is still one module deep.

Why this should be the next module:

If the author builds only ONE module this week, Softmax Jacobian is the unquestionable choice. It closes the largest hole between shipped evidence and every queued attention module.

Prerequisites Satisfied

- ✅ Attention Scaling Factor (`attention_scaling`) - completed under `modules/01_attention_scaling/`
- ✅ Softmax as a probability map (assumed calculus literacy)

Unlocks

- Multi-Head Attention backpropagation
- Causal / attention mask gradient story
- FlashAttention online-softmax correctness arguments
- Temperature scaling and sampling truncations
- Cross-entropy / KL gradient identities

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
| Completed foundations | 1 - `attention_scaling` (`.md` + `.jpg` + `.ipynb` present) |
| Queued foundations (topics.json) | 14 remaining, all status `todo` |
| Foundation curriculum covered by backlog | 15 of 50 curated foundations have backlog entries |
| Domain coverage (shipped) | Transformer Core only |
| Curriculum continuity | Fragile - softmax, residuals, masks, and MHA are missing bridges |
| Prerequisite graph | Softmax → MHA → {RoPE, KV Cache} → FlashAttention; Adam → weight decay; CE/KL → Focal / InfoNCE |
| Implementation backlog | Entire queued set lacks notebooks |
| Blog backlog | `attention_scaling` blog still `wip`; all others `todo` |
| Research backlog | Only attention scaling research marked completed |

Single largest curriculum weakness:

Missing Softmax Jacobian after Attention Scaling. Without it the repository cannot honestly progress to Multi-Head Attention, masks, or FlashAttention.

Underrepresented ML domains (shipped): Vision, Diffusion, RL, RecSys, Audio, World Models, Graph ML, Quant Finance, Causal Inference - all empty at the module layer.

---

# Foundation Gaps

Remaining foundation topics scored with `scoring.md`. Preference goes to continuity after the single shipped module.

| Rank | Topic | Score | Why Now | Unlocks |
|------|------:|--------|----------|----------|
| 1 | Softmax Jacobian (`f02`) | 39 | Direct sequel to Attention Scaling; interview staple | MHA backprop, Flash, masks, temperature |
| 2 | LayerNorm forward/backward (`f03`) | 38 | Default transformer stabilizer; independent of softmax path | RMSNorm, Pre/Post-LN, SwiGLU block |
| 3 | Residual connections (`f07`) | 38 | Identity gradient highway; missing bridge for Pre/Post-LN | Pre-LN/Post-LN, deep block composition |
| 4 | Multi-Head Attention (`f09`) | 38 | Spine of modern LLMs - wait until Softmax ships | RoPE, KV Cache, GQA, FlashAttention |
| 5 | Adam first/second moment (`f17`/`adam_optimizer`) | 37 | Optimizer interview core; no transformer prereq | Weight decay vs L2, schedules, μP |
| 6 | Causal / attention mask (`f08`) | 36 | Autoregressive legality after Softmax | ALiBi, sampling, speculative decoding |
| 7 | Cross-entropy vs KL (`f11`) | 36 | Loss identity used everywhere | Focal, label smoothing, InfoNCE, RLHF KL |
| 8 | DDPM forward process (`f48`) | 36 | Highest non-transformer portfolio unlock | Flow matching, score matching, diffusion RL |
| 9 | RMSNorm vs LayerNorm (`f04`) | 34 | Modern LLM default - blocked until LayerNorm | QK-Norm depth, Pre-RMSNorm stacks |
| 10 | InfoNCE (`f16`) | 34 | Representation learning bridge - after CE/KL | CLIP, two-tower retrieval refinements |

Foundation preference vs emerging:

Foundation wins. Softmax Jacobian outscores every accepted emerging candidate and repairs continuity. Emerging merges improve future diversity only; they do not displace this recommendation.

---

# Missing Links

Highest-impact conceptual holes given current shipped + queued state:

1. **Softmax Jacobian** - between Attention Scaling and every attention sequel
2. **Residual connections** - between LayerNorm and Pre-LN/Post-LN (`f06`)
3. **Causal / attention mask** - between Softmax and autoregressive inference modules
4. **Multi-Head Attention** - between Softmax and RoPE / KV Cache / FlashAttention
5. **ELBO / variational bound** - between probability literacy and DDPM (mitigated by merging `elbo_variational_bound`)
6. **Score matching** - between Gaussian score intuition and modern score-based / flow generative models (mitigated this week by merging `score_matching`)

These bridges outrank novelty discovery while the repository has one completed module.

---

# Emerging Candidates

Accepted only if they pass every hard gate in `scoring.md`, clear the prerequisite gate, and are suitable for derivation + canvas + from-scratch PyTorch.

| Topic | Domain | Score | Confidence | Why Interesting | Blocked On |
|--------|--------|------:|------------|-----------------|------------|
| ELBO variational bound | Diffusion / Generative | 37 | High | Missing bridge into VAEs and DDPM | - |
| Score matching | Diffusion | 36 | High | Denoising score identity; spine for score-based models | - |
| Flow matching | Diffusion | 35 | High | Vector-field transport pairs with DDPM without duplicating it | - |
| Gumbel-Softmax | Sampling / Rep. Learning | 35 | High | Differentiable categorical samples via Gumbel-Max + temperature | - |
| QK-Norm | Transformers | 34 | High | Complements 1/√d_k; controls logit variance | attention_scaling (satisfied) |
| Message passing | Graph ML | 34 | High | Aggregate-update identity; Graph ML spine | - |
| CTC loss | Audio / Speech | 34 | High | Alignment marginalization via forward-backward DP | - |
| Two-tower retrieval | RecSys | 34 | High | Dual encoders + in-batch softmax retrieval | - |
| ViT patch embedding | Vision | 34 | High | Patchify ≡ Conv2d(kernel=stride=P) | - |
| Inverse propensity weighting | Causal | 34 | High | Horvitz-Thompson ATE; causal interview staple | - |
| BPR ranking loss | RecSys | 33 | Medium | Pairwise Bayesian ranking complementary to two-tower | - |
| Kalman filter | World Models | 33 | Medium | Linear-Gaussian sequential estimation; world-model bridge | - |
| JEPA predictive objective | World Models | 33 | Medium | Latent predictive world-model entry without pixel recon | - |
| Black-Scholes PDE | Quant Finance | 33 | Medium | Replication + Itô → PDE; closed form + Monte Carlo | - |
| Mel filterbank | Audio | 32 | Medium | STFT → Mel warping; ASR front-end before CTC | - |
| Sinkhorn optimal transport | Rep. Learning | 32 | Medium | Entropic OT via matrix scaling | - |
| VICReg | Rep. Learning | 30 | Medium | Non-contrastive SSL via variance/covariance constraints | - |

---

# Blocked Candidates

Topics worth revisiting after prerequisite modules are complete. Not merged into `topics.json`.

| Topic | Waiting For |
|--------|-------------|
| GQA / MQA | Multi-Head Attention + KV Cache |
| FlashAttention-2 / FlashAttention-3 | FlashAttention |
| YaRN / ClockRoPE / other RoPE variants | RoPE |
| QLoRA / DoRA / LoRA+ | LoRA |
| Muon / Newton-Schulz orthogonalization / QK-Clip | Adam |
| Peri-LN / HybridNorm / DeepNorm residual scaling | LayerNorm + Residual connections |
| KERN / L2R / SIPS MoE routers | Mixture-of-Experts routing (`f34`) |
| Gated / differential / multi-token attention | Multi-Head Attention |
| Infini-attention / compressive memory attention | Multi-Head Attention + KV Cache |
| Path-space diffusion RL / Flow-GRPO family | DDPM + Policy gradient / REINFORCE |
| Soft Actor-Critic entropy objective | Policy gradient (`f49`) |
| AIPW / doubly robust estimators | Inverse propensity weighting |
| GAT / Graph Attention | Message passing |
| SIGReg / LeJEPA Gaussian regularizer | JEPA predictive objective |
| QK-Normed MLA / advanced QK-Norm stacks | QK-Norm + attention foundations |
| Speculative decoding (as emerging) | Already foundation `f35`; needs sampling + KV Cache |

---

# Rejected This Week

Topics considered but intentionally rejected.

| Topic | Reason |
|--------|--------|
| Model / agent / hardware launches | Product announcements, not mechanisms |
| Nested Learning / Titans / MIRAS as one module | Composite system papers; not a single derivable mechanism |
| AG-REPA and similar heuristic tricks | Paper-specific; low evergreen value |
| NT-Xent / SimCLR loss aliases | Trivial variants of InfoNCE (`f16`) |
| Straight-Through Estimator | Score 28 (<30); thin math without Gumbel pairing as standalone |
| Neural ODE adjoint method | Implementation authenticity too heavy for 100-300 line module |
| CausalMP / MPVA composite graph-causal nets | Fails authenticity and single-mechanism test; needs message passing first |
| Sparse / hierarchical memory attention variants (MSA, DHSA, Octopus) | Engineering long-context systems; require MHA + KV foundations |
| Prompt engineering / benchmarks / datasets / APIs | Explicit discovery-policy rejects |
| Speculative decoding renamed as emerging | Already curated foundation `f35`; would duplicate |

---

# Repository Coverage

| Area | Coverage |
|------|----------|
| Transformer Core | Shipped: Attention Scaling. Queued: Softmax, LayerNorm, MHA, RoPE, SwiGLU. Emerging: QK-Norm |
| Optimization | Queued: Adam, weight decay vs L2. No shipped modules |
| Loss Functions | Queued: CE vs KL, Focal, InfoNCE. Emerging: CTC, BPR, VICReg, Gumbel-Softmax |
| Diffusion | Queued: DDPM. Emerging: ELBO, Flow Matching, Score Matching |
| Reinforcement Learning | Foundation curriculum only (`f49`, `f50`); nothing queued in topics.json |
| Computer Vision | Emerging: ViT patch embedding |
| Representation Learning | Queued: InfoNCE. Emerging: JEPA, Sinkhorn OT, VICReg, Gumbel-Softmax |
| Recommendation Systems | Emerging: Two-tower retrieval, BPR ranking loss |
| World Models | Emerging: JEPA predictive objective, Kalman filter |
| Audio / Speech | Emerging: CTC loss, Mel filterbank |
| Graph ML | Emerging: Message passing |
| Quantitative Finance | Emerging: Black-Scholes PDE |
| Causal Inference | Emerging: Inverse propensity weighting |

---

# Notes

- Suggested next module remains Softmax Jacobian for the fifth consecutive editorial week while module 01 is the only shipped artifact. Objective ranking and recommendation agree.
- Prior W31/W32/W34 emerging merges still had not landed on `main`; re-validated and re-merged where still valid.
- New merges this week: `score_matching`, `bpr_ranking_loss`, `kalman_filter`, `mel_filterbank`, `vicreg`.
- Existing topics skipped (no renames, no status edits, no deletions): all manual foundation entries `01`-`15`.
- Sources unavailable: OpenAI Research index fetch timed out (HTTP timeout). Continued with NeurIPS/ICLR/ICML proceedings, Meta AI research pages, DeepMind/Google-adjacent discussion, Lilian Weng / community mechanism writing, and adopted arXiv mechanisms.
- X/Twitter (Tier 5) unused; optional and non-blocking.
- `foundation_curriculum.json` and `interest_domains` were not modified.
