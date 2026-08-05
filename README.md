# mkm-universal-root

![OSS smoke](https://github.com/mkmlab-v2/mkm-universal-root/actions/workflows/oss-smoke.yml/badge.svg)

**Who this is for:** researchers/engineers who want an **offline** check that lexicon-plane and topology-plane results stay separate on a frozen fixture (no API keys on the default path).

**What it is not:** a hosted product, a production accuracy SLA, or a drop-in substitute for frontier chat models. Not investment or medical advice.

**Fixture provenance (blunt):** the 500-pair smoke fixture is **author-curated / closed-world** for packaging + dual-plane discipline. It does **not** represent open-world language performance.

License: **MIT** — see [LICENSE](LICENSE)

## At a glance

| Try this | Where |
|----------|--------|
| **~20s repro** (no OpenAI/HF/Ollama on default path) | [Quickstart](#quickstart-3-commands) → `exit 0` + artifact JSON |
| **Third-party repro** | [Discussions #2](https://github.com/mkmlab-v2/mkm-universal-root/discussions/2) |

Observe-only UIs (if any) are **not** this repo’s benchmark — [appendix](#appendix--observe-only-ui-not-the-offline-smoke).

---

## Quickstart (3 commands)

```bash
git clone https://github.com/mkmlab-v2/mkm-universal-root.git && cd mkm-universal-root
pip install -r requirements.txt
python3 scripts/run_universal_root_oss_cursor_smoke_v1.py
```

Windows: use `py` instead of `python3`.

Expected: `reports/universal_root_oss_cursor_smoke_v1_latest.json` with `ok: true` and **separate** lexicon/topology fields (`collapsed_combined_score` stays null).

### Optional: holdout chain

For people inspecting fixtures beyond the ~20s smoke:

```bash
python3 scripts/run_universal_root_bench_5k_holdout_chain_v1.py
python3 scripts/check_universal_root_bench_5k_v1.py --strict
```

---

## Repository scope (Y1 public export)

**What you see is what you can reproduce** on the default path: clone → install → ~20s smoke → `exit 0`.

| In this repo | Not in this export |
|--------------|-------------------|
| Offline smoke runner (`scripts/run_universal_root_oss_cursor_smoke_v1.py`) | Hosted APIs, telemetry, or upload/ingestion |
| **500-pair** smoke fixture + optional **MKM-UR-Bench-5K** holdout (`tests/fixtures/nsm_41k_lexicon_crosswalk_5000_v1.json`) | Full monorepo, compression product lane, live trading |
| Topology crosswalk + gate scripts (see `docs/final/artifacts/mkm_universal_root_public_export_manifest_v1.json`) | KO shorts, clinical SOAP, auto-training on user docs |
| Dual-plane **raw** metrics; `collapsed_combined_score: null` by design | Single headline “accuracy” or global hallucination claims |
| Corpus **reference counts** (41k lexicon plane · 31,102 verse / 32,082 atom index labels) — not a warranty on open-world performance | Proprietary bulk dumps or unreleased B-track JSONL |

MIT · research PoC · not production SLA · not investment or medical advice.

---

## Fixture metrics (deep dive — author fixture; not a market claim)

**Research fixture only — not open-world warranty.**

Metrics below are **raw**, on a **500-pair fixture** (`tests/fixtures/nsm_41k_lexicon_crosswalk_500_v1.json`). Do **not** collapse lexicon and topology into one headline KPI.

| Plane | Metric | Observed (raw) |
|-------|--------|----------------|
| Lexicon 41k | `prime_hit_rate` | **99.53%** |
| Lexicon 41k | `english_only_distortion_rate` | **0.47%** |
| Topology 31k | `verse_reachable_rate` | **99.53%** |
| Walls | divergence exception cards | **2** (`heal`, `learn`) |

### Phase 1A — baseline vs dual-plane (500-pair fixture)

Compare methods on the same fixture (`428` non-control + `72` negative-control pairs). **Do not** publish the collapsed OR row (B4) as a single “accuracy” headline.

| ID | Method | Metric | Raw value |
|----|--------|--------|-----------|
| B0 | English-only naive | `english_only_hit_rate` | **78.04%** |
| B1 | Lexicon plane (41k) | `prime_hit_rate` | **99.53%** |
| B2 | Topology plane (31k) | `verse_reachable_rate` | **99.53%** |
| B3 | Dual-plane aligned (both hit) | `dual_plane_aligned_rate` | **99.53%** |
| B4 | Collapsed OR | `collapsed_or_rate` | 100% — **forbidden headline** |

Wall on B3: `2` lexicon-only-without-topology · `0` topology-only · `0` gap-both.

Reproduce comparison artifact:

```bash
python3 scripts/run_universal_root_baseline_compare_v1.py
# → reports/baseline_vs_dual_plane_v1.json (alias)
# → reports/universal_root_phase1a_baseline_compare_v1_latest.json (canonical)
```

### Named public mini-bench — UR-B0-MISS-HOLDOUT-v1

**94** English-only naive (B0) miss pairs on the same fixture — third-party evaluable holdout (not a global benchmark).

```bash
python3 scripts/build_universal_root_b0_miss_holdout_bench_v1.py
# → tests/fixtures/universal_root_b0_miss_holdout_bench_v1.json
```

### Named scaled bench — MKM-UR-Bench-5K (holdout split)

**947** holdout pairs (from **5000** auto-generated fixture; **80/20** split). Generator **v1.2.0** adds ~**12%** english-surface B0 rows (verified NSM en probes + dual-plane wiring); ~**10%** Strong's-only hard controls preserve wall divergence.

| ID | Method | Metric | Raw value (holdout) |
|----|--------|--------|---------------------|
| B0 | English-only naive | `english_only_hit_rate` | **12.21%** |
| B1 | Lexicon plane (41k) | `prime_hit_rate` | **89.20%** |
| B2 | Topology plane (stub) | `verse_reachable_rate` | **89.20%** |
| B3 | Dual-plane aligned | `dual_plane_aligned_rate` | **89.20%** |

Not a regression of the 500-pair smoke — different probe distribution and scale. Use for **holdout discipline + dual-plane margin (B3−B0 ≈ +77pp)**, not as open-world warranty.

```bash
python3 scripts/check_universal_root_bench_5k_v1.py --strict
# Pre-built artifacts: reports/universal_root_bench_5k_holdout_phase1a_v1_latest.json
```

**Dual-plane integrity:** we report planes separately — `collapsed_combined_score: null` (by design).

**Corpus reference counts** (topology index): **31,102** verse nodes · **32,082** atom nodes — see crosswalk artifact after smoke.

Reproduce command:

```bash
python3 scripts/check_hardcoded_workspace_paths_v1.py --scope oss --strict
python3 scripts/run_universal_root_oss_cursor_smoke_v1.py
```

---

## Concept (past compression craft → today's assembly kit)

| Era | Idea | This repo |
|-----|------|-----------|
| **Heavy ingestion** | Squeeze user corpora into codebooks per job | Symbolic core + gates shipped as reproducible scripts |
| **Universal Root** | Immutable rule/graph layer + optional neural draft | Fixture smoke validates topology crosswalk + wall cards **offline** |

Optional Tier 2 (not required for smoke): local SLM / DeepNSM checkpoint paths — subject to **upstream model licenses** (e.g. Meta Llama community license).

---

## Install (minimal)

```bash
pip install jsonschema pytest
python3 scripts/run_universal_root_oss_cursor_smoke_v1.py
```

---

## Disclaimer

- `[HYPO]` research PoC — no Track A · no live trading · no auto-promotion to production.
- **0.47%** is `english_only_distortion_rate` on the lexicon crosswalk fixture — **not** a universal hallucination or fake-news rate.
- Do not merge these metrics with compression KPIs, MS headlines, or unrelated lanes (e.g. KO shorts timing).

---

## Related work (research lane — not OSS smoke KPI)

Broader **Neuro → Symbolic → Human** architecture context lives in the MKM monorepo (B-track `[HYPO]` · `send_gate: HOLD`):

- **Merged synthesis (SSOT):** `docs/research/NEXT_GEN_HYBRID_AI_MKM_MERGED_LIT_REVIEW_2026-06-20.md` — Hybrid Memory / 4-Vault orchestration **roadmap only** (Y1b); not shipped in this export.
- **Y1b direction:** on-prem orchestration OS — separate from this Y1 fixture smoke; do **not** merge with compression product KPIs or MS headlines (FAIL-COMP-004).

Other monorepo-only benches (e.g. KO shorts STT timing under `scripts/run_ko_shorts_timing_compare_v1.py`) are **not** part of `mkm-universal-root` export smoke.

---

## Export bundle (maintainers)

```bash
python3 scripts/build_mkm_universal_root_public_export_bundle_v1.py --verify-only
python3 scripts/build_mkm_universal_root_public_export_bundle_v1.py --materialize
```

Manifest: `docs/final/artifacts/mkm_universal_root_public_export_manifest_v1.json`

Public push (monorepo): `scripts/Push-GitHub-Explicit.ps1 -Acknowledge` only after gates above exit 0.

---



## Appendix — methodology notes (optional)

Optional deeper docs (not required to run smoke): [Honesty Engine](docs/MKM_HONESTY_ENGINE_PUBLIC_SPEC_v1.md) · [Fact-Lock charter](docs/MKM_FACT_LOCK_CONTROL_CHARTER_PUBLIC_v1.md) · [pilot inquiry notes](docs/MKM_B2B_PILOT_INQUIRY_SPEC_PUBLIC_v1.md). These are notes, not a product SLA.

## Sponsors

GitHub Sponsors slot reserved for Y2+ maintenance — **not required** for Y1. Stars, issues, and **external smoke repro** on [Discussions #2](https://github.com/mkmlab-v2/mkm-universal-root/discussions/2) are the priority signal.

---

## Contributing fixture shards (opt-in · no telemetry)

**Not** auto-training or data upload — optional PRs of **synthetic** probe rows under human review.

See **[CONTRIBUTING.md](CONTRIBUTING.md)** · example: `tests/fixtures/contributions/pending/contributor_example_v1.json`

```bash
python3 scripts/validate_universal_root_contributor_fixture_v1.py \
  --json tests/fixtures/contributions/pending/contributor_example_v1.json
```

---

**Fixture topology stub:** Default clone ships a **fixture-aligned** verse-atom JSONL stub (`tests/fixtures/logos_verse_4d_topology_stub_v1.jsonl`, &lt;1MB) for local reproducibility on the 500-pair bench. The full ~31k-node corpus dump stays in the monorepo private B-track lane; regenerate the stub with `py scripts/extract_fixture_aligned_topology_stub_v1.py` when the fixture or audit changes.
