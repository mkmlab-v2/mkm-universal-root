# Security Policy

## Supported versions

| Version | Supported |
| ------- | --------- |
| `main` (solo OSS subset) | Yes |

This repository is **research and developer tooling** — not a hosted SaaS with SLAs.

## Reporting a vulnerability

If you believe you found a security issue in **published** MKM OSS code:

1. **Do not** open a public GitHub issue with exploit details or live secrets.
2. Email the maintainer with: affected path, reproduction steps, impact, and your contact.
3. Allow reasonable time for triage before public disclosure.

For accidental secret commits: rotate the credential immediately — scanning cannot un-leak a key.

## Secret hygiene (operators)

Before fork or public push:

```powershell
# from repo root (after git clone)
py scripts/check_mkm_secret_patterns_v1.py
powershell -NoProfile -ExecutionPolicy Bypass -File scripts/run_mkm_secret_scan_v1.ps1
powershell -NoProfile -ExecutionPolicy Bypass -File scripts/Verify-GitWorkspaceSanity.ps1
pre-commit run --all-files   # optional, after: pre-commit install
```

Never commit:

- `.env`, API keys, DPAPI exports, exchange credentials
- Local `MISSION_LOG.md`, machine-specific pointers
- Patient, grant, or trading-approval artifacts

Use `.env.example` placeholders only. Store live secrets via DPAPI (`scripts/security_agent_manager.py`) or your OS secret store — not in git.

## Automated scanning

| Tool | Role |
| ---- | ---- |
| `scripts/check_mkm_secret_patterns_v1.py` | High-confidence pattern scan (always runnable) |
| `gitleaks` + `.gitleaks.toml` | Optional deeper scan when binary is installed |
| `.pre-commit-config.yaml` | Local hook: gitleaks + pattern scan on `git commit` |

Install hooks (when `core.hooksPath` is unset):

```powershell
pre-commit install
```

When `gitleaks` is not on PATH, use the hook cache:

```powershell
pre-commit run gitleaks --all-files
```

## Scope limits

- B-track `[HYPO]` outputs are **not** operational security controls.
- MIT license — no warranty. See [README.md](README.md) disclaimer.
- **Track A live trading** remains LOCKED in this workspace; OSS does not enable exchange execution by default.

## Community FAQ (Show HN / GitHub discussions)

**Do you run a central server that ingests my code?**  
No MKM-hosted ingestion service ships in this OSS subset. Hero benches and local scripts run on your machine. If you enable Cursor/cloud LLMs, **their** egress policies still apply on the deep path.

**What leaves my machine?**  
Hero lane = structured inject/handoff JSON and lane pins — **not** full `MISSION_LOG` + CENTRAL naive paste. Deep fetch paths can still send query/subgraph text to your configured cloud IDE provider. We do **not** claim “coordinates-only for all paths” or zero cloud egress.

**Why not claim perfect routing or Cursor bill savings?**  
Measured Hero metrics are **in-repo benches** (e.g. shallow ~99.6% vs naive-paste baseline; orchestrated ~33%). `routing_oracle_gap=0.0` is **16 golden in-domain fixtures** only. OOD and Cursor proxy savings are **not** measured yet — see MERGED lit review Part X.

## Related docs

- Public copy checklist: `docs/final/PUBLIC_FACING_SECURITY_AND_IP_COPY_CHECKLIST_V1.md`
- OSS release policy: `docs/final/artifacts/mkm_solo_oss_release_policy_v1_latest.json`
- Hybrid AI related work (B-track): `docs/research/NEXT_GEN_HYBRID_AI_MKM_MERGED_LIT_REVIEW_2026-06-20.md`
