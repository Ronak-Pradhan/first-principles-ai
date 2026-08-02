# Weekly AI Math Digest

Generated: 2026-08-02 (ISO week 2026-31)

---

# Suggested Next Module

## Softmax Jacobian & Backpropagation

Overall Score: 39 / 40

Reason:

Only `modules/01_attention_scaling` has three-layer evidence (brief + canvas + notebook). Softmax is the immediate operator after the scaled logits that module justifies, and the full Jacobian \(\operatorname{diag}(p) - pp^\top\) is interview-critical, visually rich, and implementable as a tight numerical verification. It is already queued in `topics.json` with prerequisites satisfied. Shipping it extends the transformer-core spine and unlocks Multi-Head Attention, then the RoPE / KV Cache / FlashAttention path.

Foundation should be preferred here. No emerging topic beats Softmax Jacobian for long-term repository value this week: curriculum continuity from module 01 outweighs novelty. Adam and DDPM score nearly as high objectively, but they do not repair the broken attention derivation chain.

Why this should be the next module.

If the author only builds ONE module this week, Softmax Jacobian most improves repository quality. It is the missing mathematical link between shipped attention scaling and every modern attention system module still queued.

Prerequisites Satisfied

- ✅ Attention Scaling Factor (`attention_scaling`) - three-layer shipped
- ✅ Softmax as attention normalizer (used throughout module 01)
- ✅ Basic matrix calculus / chain-rule fluency assumed by the portfolio format

Unlocks

- Multi-Head Attention
- Causal / attention mask numerics (softmax after additive \(-\infty\))
- FlashAttention (via softmax + MHA + KV Cache + RoPE)
- Temperature scaling and sampling identities that reshape the same Jacobian

Estimated Effort

| Task | Hours |
|------|------:|
| Research | 3 |
| Drawing | 5 |
| Implementation | 4 |
| Blog | 5 |
| Total | 17 |

---

# Repository Health

| Signal | State |
|--------|-------|
| Completed foundations | `attention_scaling` only (`.md` + `.jpg` + `.ipynb` present) |
| Queued foundations | Softmax Jacobian, LayerNorm, MHA, RoPE, KV Cache, FlashAttention, LoRA, SwiGLU, CE vs KL, Focal Loss, Adam, Weight Decay vs L2, InfoNCE, DDPM |
| Domain coverage | Extremely transformer-core skewed; Optimization / Loss / Diffusion queued but unshipped; RL, Vision, Graph, Audio, RecSys, World Models, Quant Finance absent from shipped modules |
| Curriculum continuity | Broken after attention logits - softmax Jacobian and residuals/masks are the open bridges |
| Prerequisite graph | Softmax → MHA → (RoPE, KV Cache) → FlashAttention / GQA; LayerNorm → RMSNorm / Pre-LN vs Post-LN / SwiGLU; Adam → weight-decay variants / Muon-class optimizers; CE vs KL → Focal / InfoNCE / KL-RL |
| Implementation backlog | 14 queued foundation topics with `module_path: null` (plus newly tracked emerging) |
| Blog backlog | `attention_scaling` blog still `wip` |
| Research backlog | Softmax and every later queued topic still `research: todo` |

Single largest curriculum weakness: transformer-core spine stops at logit scaling. Softmax, Multi-Head Attention, residual highways, and causal masks are all still unshipped.

Underrepresented ML domains at the shipped-module layer: Reinforcement Learning, Computer Vision, Representation Learning, Diffusion, Recommendation Systems, Audio, World Models, Graph ML, Quantitative Finance, Causal Inference.

---

# Foundation Gaps

Evaluated remaining foundation topics with `scoring.md` (0-40). Objective ranking below; recommendation still Softmax because of continuity and satisfied prereqs.

| Rank | Topic | Score | Why Now | Unlocks |
|------|------:|--------|----------|----------|
| 1 | Softmax Jacobian & Backpropagation (`f02` / `softmax_jacobian`) | 39 | Immediate sequel to shipped attention scaling; already queued; prereqs met | Multi-Head Attention, FlashAttention path, temperature / sampling math |
| 2 | Adam from First Principles (`f17` / `adam_optimizer`) | 38 | Optimization spine; bias-correction interview classic; no hard module prereq | Weight decay vs L2, schedules, μP, modern optimizer variants (Muon blocked until Adam) |
| 3 | Diffusion Forward Process / DDPM (`f48` / `ddpm_forward_process`) | 38 | Highest portfolio generative math still queued; diversifies away from transformers | Reverse process, score matching links, Flow Matching contrast |
| 4 | Layer Normalization (`f03` / `layernorm`) | 36 | Default transformer stabilizer; subtle backward; no hard prereqs | RMSNorm, Pre-LN vs Post-LN, SwiGLU, residual signal stories |
| 5 | Residual connections as identity gradient highways (`f07`) | 36 | Missing Link - in foundation curriculum but absent from `topics.json`; universal depth identity | Pre-LN vs Post-LN, deep residual training analysis |
| 6 | Cross Entropy vs KL Divergence (`f11` / `cross_entropy_vs_kl`) | 35 | Loss spine with no hard prereqs; interview staple | Focal Loss, InfoNCE, label smoothing, KL-regularized RL |
| 7 | Multi-Head Attention (`f09` / `multi_head_attention`) | 39 objective | Architecturally critical, but Softmax Jacobian prereq not yet shipped - defer build order | RoPE, KV Cache, GQA, FlashAttention |

Notes on other remaining foundations reviewed this week (not top-5 now): Causal mask (`f08`, ~31) is a high-impact Missing Link but thinner mathematically; LoRA (`f46`, ~34) is portfolio-strong but parallel to the attention spine; RoPE / KV Cache / FlashAttention / GQA / SwiGLU / Focal Loss / Weight Decay / InfoNCE remain correctly queued behind their prerequisites; Speculative decoding (`f35`) and MoE routing (`f34`) stay foundation-queued, not re-added as emerging.

---

# Missing Links

Highest-impact conceptual holes after Attention Scaling:

1. Softmax Jacobian (`f02`) - operator between scaled logits and every attention system module
2. Residual connections (`f07`) - identity gradient highway absent from `topics.json` despite foundation curriculum entry
3. Causal / attention mask (`f08`) - additive \(-\infty\) legality before softmax; decoder spine incomplete without it
4. Multi-Head Attention (`f09`) - blocked only by Softmax; largest unlock once Softmax ships
5. Linear-layer backprop / matrix calculus (`f43`) - assumed fluency, never made explicit as a module

These bridges outrank new research for repository coherence.

---

# Emerging Candidates

Searched Tier 1-3 sources (NeurIPS / ICML / ICLR / CVPR, lab blogs, Raschka, Lilian Weng, Hugging Face) for reusable mathematical mechanisms (not model releases). Every accepted candidate scored ≥ 30 and passed hard gates.

| Topic | Domain | Score | Confidence | Why Interesting | Blocked On |
|--------|--------|------:|------------|-----------------|------------|
| Flow Matching | Diffusion | 36 | High | ODE velocity regression on linear interpolants; straight trajectories; industry-default modern generative math complementary to DDPM | - (pass; merged) |
| Message Passing / GCN aggregation | Graph ML | 36 | High | Neighborhood aggregate-update identity; fills total Graph ML absence; unlocks GAT and graph SSL later | - (pass; merged) |
| CTC Loss (forward-backward) | Audio / Speech | 34 | High | Alignment DP + marginalization; ASR interview classic; diversifies into underrepresented Audio | - (pass; merged) |
| Query-Key Normalization (QK-Norm) | Transformers | 33 | High | \(\ell_2\)/RMS normalize Q,K then learnable scale; modern LLM/ViT stability mechanism complementary to fixed \(1/\sqrt{d_k}\) | - (pass; merged) |
| Two-Tower / Dual-Encoder Retrieval | Recommendation Systems | 32 | High | Dot-product dual encoders + in-batch softmax retrieval; RecSys production spine; diversifies empty RecSys coverage | - (pass; merged) |
| VICReg (variance-invariance-covariance) | Representation Learning | 30 | Medium | Non-contrastive collapse prevention via explicit variance + covariance penalties; diversifies beyond InfoNCE | Prefer after CE/KL + InfoNCE spine starts (not hard-blocked; not merged) |
| Logit soft-capping | Transformers | 30 | Medium | \(\mathrm{soft\_cap}\cdot\tanh(z/\mathrm{soft\_cap})\); clean Gemma-style bound; thinner educational unlock than QK-Norm | Softmax intuition preferred first (not merged) |

Accepted rationales:

- Flow Matching - passes Novelty, Portfolio Fit, Authenticity; no advanced-variant prereq violation relative to DDPM (distinct ODE formulation); strong diversity win.
- Message Passing - evergreen Graph ML mechanism with clear handwritten diagrams and ~100-line PyTorch verify; largest Graph ML gap close available.
- CTC Loss - first-principles DP derivation, strong visualization (alignment lattice), implementation-friendly toy alphabet; fills Audio/Speech gap without depending on incomplete transformer spine.
- QK-Norm - directly extends shipped attention scaling; implementable from scratch; widely adopted stabilizer (ViT-22B, OLMo 2, Gemma 3).
- Two-Tower Retrieval - production RecSys mechanism with clear math (dual encoders + temperature-scaled similarity softmax); handwritten tower diagram; PyTorch dual-encoder verify; fills RecSys absence.

---

# Blocked Candidates

Topics worth revisiting after prerequisite modules are complete. Not merged into `topics.json`.

| Topic | Waiting For |
|--------|-------------|
| GQA / MQA | `multi_head_attention`, `kv_cache` |
| FlashAttention-2 / FlashAttention-3 | `flash_attention` |
| YaRN / ClockRoPE / AdaRoPE | `rope` |
| QLoRA / LoRA spectral / intruder-threshold variants | `lora` |
| Muon / Compositional Muon / QK-Clip (MuonClip) | `adam_optimizer` (then Muon base) |
| SpanNorm / HybridNorm / Peri-LN / Mix-LN / nGPT | `layernorm`, residual connections, Pre-LN vs Post-LN |
| Gated Attention / Gated DeltaNet / linear-attention hybrids | `multi_head_attention` (and broader SSM/linear-attention foundations) |
| Multi-Head Latent Attention (MLA) | `multi_head_attention`, `kv_cache` |
| STAR / ProMoE / advanced MoE routers | MoE routing load-balance foundation (`f34`) |
| P-ELBO / planner-aware discrete diffusion path learning | `ddpm_forward_process`, sampling foundations |
| SparseD / sparse attention for diffusion LMs | `multi_head_attention`, diffusion foundations |
| GRPO / group-relative advantage / GRACE-style contrastive policy opts | Policy gradient / REINFORCE (`f49`), often also InfoNCE |
| Score-smoothing / NoiseCtrl / entropy-bounded diffusion creativity controls | `ddpm_forward_process` |
| Graph Attention (GAT) | `message_passing` (newly tracked) |
| Early-interaction two-tower variants (FIT / IntTower-style) | `two_tower_retrieval` (newly tracked) |

---

# Rejected Candidates

Topics considered but intentionally rejected (fail scoring.md and/or editorial philosophy).

| Topic | Reason |
|--------|--------|
| Model releases (Gemma / OLMo / Qwen / Kimi / DiffusionGemma product posts) | Product/model launches, not reusable derivation targets |
| DiffusionGemma / Gemini Diffusion model cards | Benchmarks and model packaging, not mechanism modules |
| Hardware / kernel-only attention papers | Engineering/hardware optimization, not first-principles math |
| Tiny optimizer tweaks and hyperparameter tricks | Fail evergreen + educational bars |
| Prompt engineering / harness-engineering product loops | Outside mathematical portfolio scope |
| Empirical scaling-law fits as a module | Descriptive empiricism without a small from-scratch mechanism identity |
| CausalDiffRec / CNSDiff / LaVin-DiT-style paper stacks | Composite system papers; not a single implementable mechanism |
| Bures-Wasserstein Graph Flow Matching | Advanced graph-generative composite; wait until Flow Matching + Message Passing exist |
| WEINCE / extreme-value InfoNCE corrections | Tiny loss variant before foundation InfoNCE |
| NT-Xent / SimCLR as separate topics | InfoNCE aliases already covered by queued `info_nce` |
| Random weekly arXiv without venue adoption or clear mechanism | Tier 4 policy reject |

---

# Repository Coverage

| Area | Coverage |
|------|----------|
| Transformer Core | Thin - only Attention Scaling shipped; Softmax, LayerNorm, MHA, residuals, masks still open |
| Optimization | Queued only (Adam, weight decay); nothing shipped; Muon-class blocked |
| Loss Functions | Queued only (CE vs KL, Focal, InfoNCE); nothing shipped |
| Diffusion | Queued DDPM + newly tracked Flow Matching; nothing shipped |
| Reinforcement Learning | Curriculum only (REINFORCE, KL-regularized RL); absent from shipped modules |
| Computer Vision | Absent (convolution / BatchNorm still curriculum-only) |
| Representation Learning | Queued InfoNCE only |
| Recommendation Systems | Newly tracked Two-Tower Retrieval; nothing shipped |
| World Models | Absent |
| Audio / Speech | Newly tracked CTC Loss; nothing shipped |
| Graph ML | Newly tracked Message Passing; nothing shipped |
| Quantitative Finance | Absent |

---

# Notes

- Suggested build this week remains Softmax Jacobian even though Adam and DDPM score nearly as high objectively - repository health and curriculum continuity dominate novelty.
- Decision gate: objective ranking still favors Softmax (and MHA at equal objective once Softmax exists). Recommendation equals ranking for Softmax because prerequisites are satisfied and continuity is maximal.
- New topics merged into `topics.json`: `qk_norm`, `flow_matching`, `message_passing`, `ctc_loss`, `two_tower_retrieval`.
- Existing manual topics untouched (statuses, titles, requires preserved).
- `foundation_curriculum.json` and `interest_domains` not modified.
- Domains explored: Transformers, Diffusion, Graph ML, Representation Learning, Optimization, Inference algorithms, Audio/Speech, Recommendation Systems, Vision venue scans.
- Sources unavailable: OpenAI Research returned HTTP 403. X/Twitter was optional and not relied on for candidates (Tier 5 optional). Anthropic, DeepMind, Meta AI, Hugging Face Blog, Lilian Weng, and Sebastian Raschka were reachable.
- Prior draft weekly PRs for 2026-31 remain unmerged on other branches; this digest re-validates on current `main` state where those merges have not landed.
