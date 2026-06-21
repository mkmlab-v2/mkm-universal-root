# Contributing fixture shards — mkm-universal-root

**Status:** `[HYPO]` · `research_only` · `send_gate: HOLD`  
**Not:** hosted ingestion · auto-training on your data · telemetry · Track A promotion

---

## What we accept

**Opt-in pull requests** that add **synthetic or public-domain** lexicon probe rows — not user documents, chat logs, or PII.

| ✅ In scope | ❌ Out of scope |
|-------------|----------------|
| New probe rows (3–50 per PR) | Raw emails, clinical notes, trading data |
| Documented wall exceptions | Cloud upload / fine-tune requests |
| Negative-control tokens | Merging lexicon + topology into one KPI |

**Frozen canonical bench (maintainers only):** `tests/fixtures/nsm_41k_lexicon_crosswalk_500_v1.json` — do not overwrite in drive-by PRs.

---

## File layout

```
tests/fixtures/contributions/pending/
  nsm_41k_lexicon_crosswalk_contrib_<your_id>_v1.json
```

Schema: `nsm_41k_lexicon_crosswalk_contrib_v1` — see `tests/fixtures/contributions/pending/contributor_example_v1.json`.

Each sample row must include:

- `prime_en` (lowercase ASCII)
- `probe_tokens` (1–5 strings, no PII)
- `contributor_provided: true`
- `customer_provided: false`
- `labels`: `contributor_provided`, `research_only`, `universal_root_fixture_v1`
- `source_note` (how the row was derived)

---

## Before you open a PR

Run locally (**no data leaves your machine**):

```bash
pip install -r requirements.txt
python3 scripts/run_universal_root_oss_cursor_smoke_v1.py
python3 scripts/validate_universal_root_contributor_fixture_v1.py \
  --json tests/fixtures/contributions/pending/<your_shard>.json
python3 scripts/run_universal_root_contributor_bench_v1.py \
  --shard tests/fixtures/contributions/pending/<your_shard>.json
python3 -m pytest tests/test_universal_root_contributor_fixture_v1.py -q
```

Paste exit 0 summaries in the PR description.

---

## Review gates (maintainers)

1. Validate + bench green · no PII · plane separation preserved  
2. Overlap with canonical 500 → explicit review (not auto-reject)  
3. Merge to `pending/` or exception-card only — **human** promotion to canonical bench  
4. **No** auto SEND · **no** live trading · **no** implied production SLA  

---

## Positioning (please do not overclaim)

We do **not** get smarter automatically as user count grows. Growth path:

**Reproduce → trust → optional fixture PR → human-gated bench expansion**

Forbidden in PR text: “data flywheel,” “network effect on model quality,” “0.47% global hallucination rate.”

---

## Questions

Open a GitHub issue with reproduce command output. Do not attach private corpora.

*Contributor guide v1 · MIT · research PoC only*
