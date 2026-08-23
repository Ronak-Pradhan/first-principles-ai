# Weekly AI Math Digest

Generated: 2026-08-23 (2026-W34)

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
5. **ELBO / variational bound** - between probability literacy and DDPM (mitigated this week by merging `elbo_variational_bound`)

These bridges outrank novelty discovery while the repository has one completed module.

---

# Emerging Candidates

Accepted only if they pass every hard gate in `scoring.md`, clear the prerequisite gate, and are suitable for derivation + canvas + from-scratch PyTorch.

| Topic | Domain | Score | Confidence | Why Interesting | Blocked On |
|--------|--------|------:|------------|-----------------|------------|
| `qk_norm` | Transformers | 34 | High | Normalize Q/K before dots; controls logit variance beyond 1/√d_k; production LLM stabilizer | - |
| `elbo_variational_bound` | Diffusion / Generative | 37 | High | Evidence lower bound identity; missing bridge into DDPM and VAEs | - |
| `flow_matching` | Diffusion | 35 | High | Continuous normalizing flows via vector-field regression; pairs with DDPM without duplicating it | - |
| `gumbel_softmax` | Sampling / Discrete Latents | 35 | High | Gumbel-Max + temperature softmax relaxation; differentiable categorical samples | - |
| `message_passing` | Graph ML | 34 | High | Aggregate-update identity; first Graph ML spine | - |
| `ctc_loss` | Audio / Speech | 34 | High | Forward-backward DP over alignments; ASR interview staple | - |
| `two_tower_retrieval` | Recommendation | 34 | High | Dual-encoder + in-batch softmax retrieval math | - |
| `vit_patch_embedding` | Vision | 34 | High | Patchify ≡ Conv2d(kernel=stride=P); Vision transformer entry | - |
| `inverse_propensity_weighting` | Causal Inference | 34 | High | Horvitz-Thompson ATE estimator; causal spine | - |
| `jepa_predictive_objective` | World Models | 33 | Medium | Latent view-prediction identity; world-model entry without pixel reconstruction | - |
| `black_scholes_pde` | Quantitative Finance | 33 | Medium | Replication + Itô PDE + closed form / MC check | - |
| `sinkhorn_optimal_transport` | Representation / Generative | 32 | Medium | Entropic OT via Sinkhorn scaling; WGAN / matching bridge | - |

---

# Blocked Candidates

Worth revisiting after prerequisite modules are complete. Not merged into `topics.json`.

| Topic | Waiting For |
|--------|-------------|
| GQA / MQA memory-quality tradeoff | Multi-Head Attention + KV Cache |
| FlashAttention-2 / FlashAttention-3 | FlashAttention |
| YaRN / NTK-aware RoPE scaling | RoPE |
| QLoRA / LoRA+ / DoRA | LoRA |
| Muon / Compositional Muon / QK-Clip | Adam |
| KERN / Nadaraya-Watson MoE router | Mixture-of-Experts load-balance foundation (`f34`) |
| L2R / SIPS Lipschitz MoE routing | MoE load-balance + LayerNorm/RMSNorm |
| Peri-LN / HybridNorm / SpanNorm | LayerNorm + Residual connections |
| Gated attention / differential attention hybrids | Multi-Head Attention |
| Path-space diffusion RL / DMPO / LaDi-RL | DDPM + Policy Gradient / REINFORCE |
| AIPW / doubly robust estimators | Inverse propensity weighting (module complete) |
| GAT / Graph Attention | Message passing (module complete) |
| QK-Normed MLA absorption trick | QK-Norm + Multi-Head / latent attention foundations |

---

# Rejected This Week

| Topic | Reason |
|--------|--------|
| Model / agent product launches (AlphaEvolve narratives, IMO contest framing) | Not a reusable mathematical mechanism |
| Nested Learning / Titans / MIRAS as a single module | Composite system paper; fails from-scratch authenticity and 100-300 line portfolio fit |
| AG-REPA / FoG-A layer selection | Training heuristic on top of flow matching; not a first-principles primitive |
| NT-Xent / SimCLR loss naming | Alias of InfoNCE already in foundation backlog |
| Speculative decoding (as emerging) | Already foundation `f35`; not novel to backlog |
| Hardware kernel announcements / HBM tiling product posts | Engineering/hardware, not derive-and-implement math |
| Prompt engineering / benchmark suites / dataset releases | Fail portfolio-fit and authenticity gates |
| Tiny MoE router activations without MoE foundation | Prerequisite violation + variant chasing |

---

# Repository Coverage

| Area | Coverage |
|------|----------|
| Transformer Core | Weak shipped (Attention Scaling only); Softmax/MHA/LN/Residuals still gaps |
| Optimization | Queued only (Adam, weight decay) |
| Loss Functions | Queued (CE/KL, Focal); emerging adds CTC, Gumbel-Softmax, ELBO |
| Diffusion | Queued DDPM; emerging Flow Matching + ELBO bridge |
| Reinforcement Learning | Foundation only (`f49`/`f50`); no backlog module yet |
| Computer Vision | Emerging ViT patch embedding |
| Representation Learning | Queued InfoNCE; emerging Sinkhorn OT |
| Recommendation Systems | Emerging two-tower retrieval |
| World Models | Emerging JEPA predictive objective |
| Audio / Speech | Emerging CTC |
| Graph ML | Emerging message passing |
| Quantitative Finance | Emerging Black-Scholes PDE |
| Causal Inference | Emerging IPW |

---

# Notes

- Suggested next module unchanged in substance from 2026-W31/W32: Softmax Jacobian still unshipped; recommendation stands.
- New topics merged into `topics.json` this week: `qk_norm`, `elbo_variational_bound`, `flow_matching`, `gumbel_softmax`, `message_passing`, `ctc_loss`, `two_tower_retrieval`, `vit_patch_embedding`, `inverse_propensity_weighting`, `jepa_predictive_objective`, `black_scholes_pde`, `sinkhorn_optimal_transport`.
- Existing topics skipped (no renames, deletes, or manual status edits): all ids `01`-`15`.
- Prior W31/W32 emerging merges had not landed on `main`; re-validated and merged again where still valid.
- Sources unavailable: OpenAI Research site returned HTTP 403; discovery continued via DeepMind/Google Research, Meta AI, conference proceedings, Lilian Weng, and arXiv only when mechanism-level and widely adopted.
- X/Twitter (Tier 5) not required this week; not used.
- `foundation_curriculum.json` and `interest_domains` were not modified.
