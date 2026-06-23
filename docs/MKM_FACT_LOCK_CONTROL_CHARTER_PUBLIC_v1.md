# MKM Fact-Lock Control Charter (Public v1)

**Status:** `research_only` · fixture bench only · **not** legal advice · **not** production SLA  
**Send gate:** `HOLD`  
**Companion:** [MKM Honesty Engine Spec](MKM_HONESTY_ENGINE_PUBLIC_SPEC_v1.md)

This charter states **what we measure**, **what we refuse to merge**, and **how to reproduce** — without internal graph dumps, orchestration paths, or open-world accuracy claims.

---

## 1. Measurement contract

| Rule | Meaning |
|------|---------|
| **Dual-plane split** | Report lexicon (B1) and topology (B2) separately; B3 = both hit. |
| **No collapsed headline** | `collapsed_combined_score: null` by design; **B4 forbidden** in public copy. |
| **Fixture scope** | Metrics are on **named JSON fixtures**, not the open internet or full private corpus. |
| **Artifact binding** | Headline numbers must match `*_latest.json` after reproduce commands exit 0. |
| **Holdout discipline** | Scaled bench uses deterministic **80/20** split — report holdout slice, not train. |

---

## 2. Named benches (public export)

| Bench | Pairs | Role |
|-------|-------|------|
| **500-pair smoke** | 500 | OSS CI default · ~20s reproduce |
| **UR-B0-MISS-HOLDOUT-v1** | 94 | B0-miss evaluable slice on 500 fixture |
| **MKM-UR-Bench-5K** | 5000 full · **947 holdout** | Scaled dual-plane holdout (generator v1.2.0: english-surface B0 slice + dual-plane wiring) |

**5K holdout (raw · 947 pairs · non_control 917):**

| ID | Metric | Value |
|----|--------|-------|
| B0 | `english_only_hit_rate` | **12.21%** |
| B1 | `prime_hit_rate` | **89.20%** |
| B2 | `verse_reachable_rate` | **89.20%** |
| B3 | `dual_plane_aligned_rate` | **89.20%** |

**B0 slice (v1.2.0):** ~**12%** `massive_gen_english_surface_b0` rows use verified NSM-style English probes (dual-plane wired). Remaining rows are atom-linked / Strong's-style; **~10%** hard Strong's-only controls preserve wall divergence. Margin = **B3 − B0** on the **same holdout** (currently **+76.99pp**), not vs 500-pair smoke.

**Wall on holdout:** `gap_both_planes` **99** · `aligned_both_planes` **818**.

---

## 3. Forbidden public claims

- Global hallucination rate · fake-news firewall · regulatory-grade accuracy  
- GPT-4 replacement · sub-second GraphRAG at scale (not benchmarked here)  
- Single merged “accuracy” from B1+B2 or B4  
- Full 31k topology dump · proprietary lemma edges · auto-training on user uploads  
- Track A live trading · SEND auto-enable · medical device claims  

---

## 4. Reproduce (5K holdout)

```bash
python3 scripts/run_universal_root_bench_5k_holdout_chain_v1.py
python3 scripts/check_universal_root_bench_5k_v1.py --strict
```

Artifacts: `reports/universal_root_bench_5k_holdout_phase1a_v1_latest.json`

---

*Public charter v1 · 2026-06-23 · `send_gate: HOLD`*
