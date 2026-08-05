# mkm-universal-root

![OSS smoke](https://github.com/mkmlab-v2/mkm-universal-root/actions/workflows/oss-smoke.yml/badge.svg)

**Who this is for:** people who want a local **regression smoke** with **two checks that can fail independently** (term-map vs path/graph) on a frozen fixture — no OpenAI/HF/Ollama on the default path.

**Concrete example:** same item can be `lexicon_hit=true` and `topology_reachable=false` (term mapped, path constraint fails). Smoke reports both; it does **not** OR them into one score.

**What it is not:** hosted product · production accuracy SLA · frontier-chat substitute · investment/medical advice.

**Fixture:** `tests/fixtures/nsm_41k_lexicon_crosswalk_500_v1.json` — **author-curated regression fixture** (closed-world), not general language performance.

License: **MIT** — see [LICENSE](LICENSE)

## Quickstart

```bash
git clone https://github.com/mkmlab-v2/mkm-universal-root.git && cd mkm-universal-root
pip install -r requirements.txt
python3 scripts/run_universal_root_oss_cursor_smoke_v1.py
```

Windows: `py` instead of `python3`.

**Inputs:** the 500-pair fixture JSON + local topology stub under `tests/fixtures/`.  
**Output:** `reports/universal_root_oss_cursor_smoke_v1_latest.json` (`ok: true`, separate lexicon/topology fields; `collapsed_combined_score` stays null).

Third-party repro: [Discussions #2](https://github.com/mkmlab-v2/mkm-universal-root/discussions/2).

## Scope

| In this export | Not in this export |
|----------------|--------------------|
| Offline smoke runner + fixture | Hosted APIs / telemetry |
| Separate check results in JSON | Live trading · compression product · full monorepo |

## Optional extras

Larger author fixtures under `scripts/` / `tests/fixtures/` are optional inspect tools — still closed-world.

```bash
python3 scripts/run_universal_root_bench_5k_holdout_chain_v1.py
python3 scripts/check_universal_root_bench_5k_v1.py --strict
```

## Appendix — auditor numbers only (skip on first read)

**Not open-world performance.** Phase 1A recompute anchors for disk auditors:

| ID | Metric | Raw |
|----|--------|-----|
| B0 | `english_only_hit_rate` | **78.04%** |
| B3 | `dual_plane_aligned_rate` | **99.53%** |
| — | `prime_hit_rate` / `verse_reachable_rate` | **99.53%** |
| — | `english_only_distortion_rate` | **0.47%** |
| B4 | collapsed OR | **forbidden headline** |

```bash
python3 scripts/run_universal_root_baseline_compare_v1.py
python3 scripts/check_hardcoded_workspace_paths_v1.py --scope oss --strict
```

## Contributing / maintainers

Synthetic fixture PRs: [CONTRIBUTING.md](CONTRIBUTING.md).  
Bundle: `python3 scripts/build_mkm_universal_root_public_export_bundle_v1.py --materialize`
