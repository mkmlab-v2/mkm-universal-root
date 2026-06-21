# mkm-universal-root

**Neuro-symbolic integrity kit for developers** — pre-built symbolic grids (lexicon + corpus topology) with optional local SLM paths. **Not** a hosted ingestion SaaS · **not** a GPT-4 replacement · **not** investment or medical advice.

License: **MIT** — see [LICENSE](LICENSE)

---

## Clone → 20 seconds → exit 0

No Hugging Face token · no Ollama · no cloud API on the default smoke path.

```bash
# from repo root after git clone (Windows: py instead of python3)
python3 scripts/run_universal_root_oss_cursor_smoke_v1.py
```

Artifact: `reports/universal_root_oss_cursor_smoke_v1_latest.json`

Launch Gate #1 (OSS path audit) runs inside the smoke unless you pass `--skip-path-audit`.

---

## What this proves (fixture bench — not production SLA)

**Track B `[HYPO]` · `research_only` · `send_gate: HOLD`**

Metrics below are **raw**, on a **500-pair fixture** (`tests/fixtures/nsm_41k_lexicon_crosswalk_500_v1.json`). Do **not** collapse lexicon and topology into one headline KPI.

| Plane | Metric | Observed (raw) |
|-------|--------|----------------|
| Lexicon 41k | `prime_hit_rate` | **99.53%** |
| Lexicon 41k | `english_only_distortion_rate` | **0.47%** |
| Topology 31k | `verse_reachable_rate` | **99.53%** |
| Walls | divergence exception cards | **2** (`heal`, `learn`) |

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

## Related research (separate lane — not this smoke)

Korean shorts STT timing experiments live under `scripts/run_ko_shorts_timing_compare_v1.py` in the full MKM monorepo — **not** part of `mkm-universal-root` export smoke.

---

## Export bundle (maintainers)

```bash
python3 scripts/build_mkm_universal_root_public_export_bundle_v1.py --verify-only
python3 scripts/build_mkm_universal_root_public_export_bundle_v1.py --materialize
```

Manifest: `docs/final/artifacts/mkm_universal_root_public_export_manifest_v1.json`

Public push (monorepo): `scripts/Push-GitHub-Explicit.ps1 -Acknowledge` only after gates above exit 0.
