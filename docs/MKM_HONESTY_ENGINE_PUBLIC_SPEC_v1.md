# MKM Honesty Engine Specification (v1.0)

**Status:** `research_only` · **Environment:** fixture bench only · **License:** MIT  
**Send gate:** `HOLD` — not production SLA · not investment or medical advice

This document is a **public distillation** of how MKM reports neuro-symbolic integrity on a **closed 500-pair fixture**. It is **not** internal orchestration documentation, proprietary graph dumps, or a claim of global model superiority.

---

## 1. Core principles (five rules)

1. **Disaggregated reporting** — Lexicon-plane and topology-plane metrics are reported **separately**. `collapsed_combined_score: null` is intentional: do not merge planes into one headline KPI. Collapsed OR (B4) is **forbidden** as a public “accuracy” line.

2. **Immutable baseline anchor** — Baseline B0 (English-only naive) logic and the fixture file are pinned by SHA256 in integrity gates. Do not retune the control group to inflate margins.

3. **Artifact-driven copy** — README percentages must match reproduced JSON artifacts (`*_latest.json`). If integrity checks fail, export/push gates block publication.

4. **Deterministic boundary gating** — Failed integrity or gate scripts return **non-zero exit codes**. Warnings alone do not substitute for blocking bad artifacts.

5. **Sandbox containment** — Default OSS path is offline smoke on the fixture. Live showroom URLs are **read-only demos**, not benchmarks. Full corpus graphs and proprietary edges stay outside this export.

---

## 2. What this repo proves (fixture scope)

| ID | Method | Metric | Raw (fixture) |
|----|--------|--------|----------------|
| B0 | English-only naive | `english_only_hit_rate` | **78.04%** |
| B1 | Lexicon plane | `prime_hit_rate` | **99.53%** |
| B2 | Topology plane | `verse_reachable_rate` | **99.53%** |
| B3 | Dual-plane aligned | `dual_plane_aligned_rate` | **99.53%** |
| B4 | Collapsed OR | `collapsed_or_rate` | 100% — **do not headline** |

**Named mini-bench:** UR-B0-MISS-HOLDOUT-v1 — **94** B0-miss pairs (evaluable holdout slice, not a global benchmark).

**Corpus reference counts** (labels only): 31,102 verse nodes · 32,082 atom index labels — **not** a warranty on open-world performance. Export ships a **&lt;1MB topology stub** aligned to the fixture, not the full private graph.

---

## 3. Reproduce (no API keys)

```bash
pip install -r requirements.txt
python3 scripts/run_universal_root_oss_cursor_smoke_v1.py          # ~20s · exit 0
python3 scripts/run_universal_root_baseline_compare_v1.py          # Phase 1A table artifact
python3 scripts/build_universal_root_b0_miss_holdout_bench_v1.py # 94-pair holdout fixture
```

Windows: use `py` instead of `python3`.

---

## 4. Explicitly out of scope

- Hosted ingestion SaaS, telemetry, or auto-training on user documents  
- GPT-4 / “global hallucination firewall” / killer-model claims  
- Track A live trading or SEND automation  
- Merging compression KPI (~47.5% enterprise lane) with fixture plane metrics  
- Full Gem / monorepo orchestration specs (internal only)

---

## 5. Live demos (observation only)

Read-only showroom pages are linked from the [README](README.md). They illustrate Track C UI; **reproducible claims** for this repo remain the offline fixture path above.

---

*Public spec v1.0 · 2026-06-22 · `send_gate: HOLD`*
