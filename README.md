# mkm-universal-root

![OSS smoke](https://github.com/mkmlab-v2/mkm-universal-root/actions/workflows/oss-smoke.yml/badge.svg)

**Who this is for:** researchers/engineers who want an **offline regression smoke** that runs **two checks that can fail independently** (term-map vs path/graph) on a frozen fixture — no OpenAI/HF/Ollama on the default path.

**Practical point:** catches “term mapped OK but path constraint wrong” (and the reverse) without collapsing those into one accuracy number.

**What it is not:** a hosted product · a production accuracy SLA · a drop-in substitute for frontier chat models · investment or medical advice.

**Fixture provenance (blunt):** `tests/fixtures/nsm_41k_lexicon_crosswalk_500_v1.json` is an **author-curated regression fixture** (closed-world). It is **not** evidence of general language performance.

License: **MIT** — see [LICENSE](LICENSE)

## At a glance

| Try this | Where |
|----------|--------|
| **~20s repro** | [Quickstart](#quickstart) → `exit 0` + artifact JSON |
| **Third-party repro** | [Discussions #2](https://github.com/mkmlab-v2/mkm-universal-root/discussions/2) |

## Quickstart

```bash
git clone https://github.com/mkmlab-v2/mkm-universal-root.git && cd mkm-universal-root
pip install -r requirements.txt
python3 scripts/run_universal_root_oss_cursor_smoke_v1.py
```

Windows: use `py` instead of `python3`.

Expected artifact: `reports/universal_root_oss_cursor_smoke_v1_latest.json` with `ok: true` and **separate** lexicon / topology fields (`collapsed_combined_score` stays null).

Example shape (illustrative):

```json
{"ok": true, "metrics": {"raw_lexicon_prime_hit_rate": 0.9953, "topology_verse_reachable_rate": 0.9953, "wall_exception_count": 2}}
```

## Scope

| In this export | Not in this export |
|----------------|--------------------|
| Offline smoke runner + 500-pair fixture | Hosted APIs / telemetry / upload |
| Scripts that print separate check results | Live trading · compression product surfaces · full monorepo |

MIT · research PoC · not production SLA.

## Optional extras (after smoke)

Extra fixture-inspect scripts exist under `scripts/` (larger author fixtures). They are **optional** and still closed-world — not a market claim.

```bash
python3 scripts/run_universal_root_bench_5k_holdout_chain_v1.py
python3 scripts/check_universal_root_bench_5k_v1.py --strict
```

## Appendix A — author-fixture regression numbers (skip unless auditing)

**Do not treat as open-world performance.** Kept here so auditors can recompute Phase 1A values from disk artifacts.

500-pair fixture (`tests/fixtures/nsm_41k_lexicon_crosswalk_500_v1.json`):

| Plane | Metric | Observed (raw) |
|-------|--------|----------------|
| Lexicon | `prime_hit_rate` | **99.53%** |
| Lexicon | `english_only_distortion_rate` | **0.47%** |
| Topology | `verse_reachable_rate` | **99.53%** |
| Walls | divergence exception cards | **2** (`heal`, `learn`) |

Phase 1A compare (same fixture; **B4 forbidden as headline**):

| ID | Method | Metric | Raw value |
|----|--------|--------|-----------|
| B0 | English-only naive | `english_only_hit_rate` | **78.04%** |
| B1 | Lexicon | `prime_hit_rate` | **99.53%** |
| B2 | Topology | `verse_reachable_rate` | **99.53%** |
| B3 | Both aligned | `dual_plane_aligned_rate` | **99.53%** |
| B4 | Collapsed OR | `collapsed_or_rate` | 100% — **forbidden headline** |

```bash
python3 scripts/run_universal_root_baseline_compare_v1.py
python3 scripts/check_hardcoded_workspace_paths_v1.py --scope oss --strict
python3 scripts/run_universal_root_oss_cursor_smoke_v1.py
```

Larger author fixtures (optional inspect only): `tests/fixtures/nsm_41k_lexicon_crosswalk_5000_v1.json` · B0-miss subset builder `scripts/build_universal_root_b0_miss_holdout_bench_v1.py`.

## Appendix B — observe-only UI (not the offline smoke)

Optional read-only pages. **Not** this repo’s reproducible benchmark.

| What | URL |
|------|-----|
| Logos Studio | https://logos.jema-ai.com/logos-research/studio?q=job_job_suffering_reason&autorun=1&demo=1 |
| Showroom oracle | https://api.jemaai.cloud/public_showroom_logos_oracle_v6.html?product=1 |

## Appendix C — notes / contributing

Optional docs (not required to run smoke): [Honesty Engine](docs/MKM_HONESTY_ENGINE_PUBLIC_SPEC_v1.md) · [Fact-Lock charter](docs/MKM_FACT_LOCK_CONTROL_CHARTER_PUBLIC_v1.md) · [pilot notes](docs/MKM_B2B_PILOT_INQUIRY_SPEC_PUBLIC_v1.md).

Contributing: synthetic fixture PRs only — see [CONTRIBUTING.md](CONTRIBUTING.md).

Maintainers:

```bash
python3 scripts/build_mkm_universal_root_public_export_bundle_v1.py --verify-only
python3 scripts/build_mkm_universal_root_public_export_bundle_v1.py --materialize
```

**Fixture topology stub:** `tests/fixtures/logos_verse_4d_topology_stub_v1.jsonl` ships for local repro; full corpus dumps stay out of this export.
