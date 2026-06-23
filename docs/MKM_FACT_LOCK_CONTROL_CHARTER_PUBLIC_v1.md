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
| **MKM-UR-Bench-5K** | 5000 full · **988 holdout** | Scaled dual-plane holdout (`atom_id` + `topology_probe_tokens`) |

**5K holdout (raw · 988 pairs · non_control 958):**

| ID | Metric | Value |
|----|--------|-------|
| B0 | `english_only_hit_rate` | **0.00%** |
| B1 | `prime_hit_rate` | **84.86%** |
| B2 | `verse_reachable_rate` | **84.86%** |
| B3 | `dual_plane_aligned_rate` | **84.86%** |

**Why B0 = 0% on 5K holdout:** rows wire Strong's / atom-linked probes — not English surface tokens. B0 is still reported; do not hide it. Margin narrative = **B3 − B0** on the **same holdout**, not vs 500-pair smoke.

**Wall on holdout:** `gap_both_planes` **145** (Strong's-only hard controls · ~15%) · `aligned_both_planes` **813**.

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
