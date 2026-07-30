# Weekly AI Math Digest

Generated: 2026-07-30

---

# Suggested Next Module

## Softmax Jacobian & Backpropagation

Overall Score: 39 / 40

Reason:

Only `modules/01_attention_scaling` has three-layer evidence (brief + canvas + notebook). Softmax is the immediate operator after the scaled logits that module justifies, and the full Jacobian \(\operatorname{diag}(p) - pp^\top\) is interview-critical, visually rich, and implementable as a tight numerical verification. It is already queued in `topics.json` with prerequisites satisfied. Shipping it extends the transformer-core spine and unlocks Multi-Head Attention, then the RoPE / KV Cache / FlashAttention path. Foundation should be preferred here; no emerging topic beats this for long-term portfolio value this week.

Why this should be the next module.

If the author only builds ONE module this week, Softmax Jacobian most improves repository quality: it is the missing mathematical link between shipped attention scaling and every modern attention system module still queued.

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

# Foundation Gaps

| Rank | Topic | Score | Why Now | Unlocks |
|------|------:|--------|----------|----------|
| 1 | Softmax Jacobian & Backpropagation (`f02` / `softmax_jacobian`) | 39 | Immediate sequel to shipped attention scaling; already queued; prereqs met | Multi-Head Attention, FlashAttention path, temperature / sampling math |
| 2 | Layer Normalization (`f03` / `layernorm`) | 36 | Default transformer stabilizer; subtle backward; no hard prereqs | RMSNorm, Pre-LN vs Post-LN, SwiGLU, residual signal stories |
| 3 | Residual connections as identity gradient highways (`f07`) | 35 | Missing Link - not yet in `topics.json`; universal depth identity across CNN and Transformer stacks | Pre-LN vs Post-LN, deep residual training analysis |
| 4 | Cross Entropy vs KL Divergence (`f11` / `cross_entropy_vs_kl`) | 34 | Loss spine with no hard prereqs; interview staple | Focal Loss, InfoNCE, label smoothing, KL-regularized RL |
| 5 | Adam from First Principles (`f17` / `adam_optimizer`) | 34 | Optimization spine; bias-correction interview classic | Weight decay vs L2, schedules, μP, modern optimizer variants |

---

# Emerging Candidates

| Topic | Domain | Score | Why Interesting | Blocked On |
|--------|--------|------:|-----------------|------------|
| Query-Key Normalization (QK-Norm) | Transformers | 33 | \(\ell_2\)/RMS normalize Q,K then learnable scale; replaces fixed \(1/\sqrt{d_k}\) for logit control; used in ViT-22B, OLMo 2, Gemma 3 | - (pass; merged) |
| Flow Matching | Diffusion | 36 | ODE velocity regression on linear interpolants; straight trajectories; industry-default modern generative math complementary to DDPM | - (pass; merged) |
| Logit soft-capping | Transformers | 30 | \(\mathrm{soft\_cap}\cdot\tanh(z/\mathrm{soft\_cap})\); Gemma 2 attention/final logit bound; clean but thinner than QK-Norm | Softmax intuition preferred first (not hard-blocked) |

---

# Blocked Candidates

Topics worth revisiting after prerequisite modules are complete.

| Topic | Waiting For |
|--------|-------------|
| SpanNorm / SiameseNorm (Pre/Post-Norm reconciliation) | `layernorm`, residual connections, Pre-LN vs Post-LN |
| Score smoothing (diffusion interpolation / creativity) | `ddpm_forward_process` |
| GRPO group-relative advantage | Policy gradient / REINFORCE baseline (`f49`) |
| GQA / MQA | `multi_head_attention`, `kv_cache` |
| ClockRoPE / YaRN / AdaRoPE | `rope` |
| FlashAttention-2 / FlashAttention-3 | `flash_attention` |
| LoRA spectral / intruder-threshold variants | `lora` |
| nGPT (hypersphere-normalized Transformer) | `layernorm`, RMSNorm |
| ProMoE / diffusion MoE routing variants | MoE routing foundation, `ddpm_forward_process` |
| Muon / SAM spectral optimizer variants | `adam_optimizer` |

---

# Rejected This Week

Topics considered but intentionally rejected.

| Topic | Reason |
|--------|--------|
| WEINCE / extreme-value InfoNCE corrections | Tiny loss variant before foundation InfoNCE; fails evergreen + educational bar |
| DiffusionGemma / model releases | Product/model launch, not a reusable derivation target |
| Attention-as-reverse-diffusion geometric control law | Speculative framing without clear small PyTorch module contract |
| Hardware / kernel-only attention papers | Engineering/hardware optimization, not first-principles math |
| Benchmarks, datasets, API announcements | Outside portfolio scope per `sources.md` |
| Prompt engineering / product features | Not mathematical mechanisms |

---

# Repository Coverage

| Area | Coverage |
|------|----------|
| Transformer Core | Thin - only Attention Scaling shipped; Softmax, LayerNorm, MHA, residuals still open |
| Optimization | Queued only (Adam, weight decay); nothing shipped |
| Loss Functions | Queued only (CE vs KL, Focal, InfoNCE); nothing shipped |
| Diffusion | Queued DDPM + newly tracked Flow Matching; nothing shipped |
| Reinforcement Learning | Curriculum only (REINFORCE, KL-regularized RL); absent from shipped modules |
| Computer Vision | Absent (convolution / BatchNorm still curriculum-only) |
| Representation Learning | Queued InfoNCE only |
| Recommendation Systems | Absent |
| World Models | Absent |
| Audio / Speech | Absent |
| Graph ML | Absent |
| Quantitative Finance | Absent |

---

# Notes

- New topics merged into topics.json: `qk_norm`, `flow_matching`
- Existing topics skipped: all manual foundation entries; FlashAttention and LoRA remain intentionally queued
- Missing Links surfaced: Residual connections (`f07`), Causal / attention mask (`f08`), Multi-Head Attention (queued but gated on Softmax)
- Sources unavailable: Hugging Face Blog fetch timed out; X/Twitter lookups skipped (unreachable this run)
- Domains explored: Transformers, Diffusion / generative, Representation Learning, Reinforcement Learning, Lab blogs (Google Research / DeepMind), venue tracks (ICML / ICLR / EMNLP)
- Foundation preferred over emerging for the Suggested Next Module; emerging merges diversify Diffusion without displacing the Softmax spine recommendation
