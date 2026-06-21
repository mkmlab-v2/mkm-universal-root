# Neuro-Symbolic B2B 구조 검증 — 대외 1페이지 (초안 v1)

**상태:** `[HYPO]` · `research_only` · Track B PoC — **법무 검토 전** · **투자·의료·신학 단정 금지**  
**정렬:** `docs/final/PUBLIC_FACING_SECURITY_AND_IP_COPY_CHECKLIST_V1.md` · `TRACK_C_IP_BUSINESS_PLAN_2026-04-17.md` §3.1.8

---

## 한 줄 가치

**LLM 초안 + 결정론적 논리 배관 + 인간 승인 게이트** — 제안서·전략 문서에서 **구조적 모순·경로 누락 후보**를 artifact-bound로 탐지한다.  
**교리·신학 내용이 아니라 검증 topology(인용 잠금·규칙·경로 감사)만** 이식한다.

---

## 무엇을 하지 않는가 (면책)

- 투자 조언·수익 보장·「AI가 성경으로 똑똑해짐」·모델 파인튜닝 주장 **아님**
- MS 1-pager 헤드라인(압축 %·토큰 수)과 **합산·단일 KPI 금지** (FAIL-COMP-004)
- Track A 승격·실매매·자동 송출 **없음** — `human-in-the-loop` 필수

---

## 문제 정의 (비유 — 설명용)

| 일반 웹 코퍼스 | 고전·장문 말뭉치 상호참조 그래프 |
|----------------|----------------------------------|
| 정보는 많으나 논리 연결이 듬성함 | 장기간 정합성 압력 → **multi-hop evidence path** 밀도 높음 |
| 벡터 유사도 검색 위주 | **그래프 경로 + 규칙 게이트**로 검증 가능 |

→ 비즈니스 문서에 이식하는 것은 **「내용」이 아니라 「검증 구조」**이다.

---

## Neuro-Symbolic 하이브리드 (우리 방식)

| 층 | 역할 | MKM PoC |
|----|------|---------|
| **Neuro** | LLM 초안·통찰 문장 생성 | Ollama distill · multi-insight synthesis |
| **Symbolic** | verse/clause 그래프·규칙·경로 강제 | citation_lock · Alpha/Beta chain · V(Sᵢ) gate |
| **Human** | 송출·법무·중요 변수 승인 | HITL checkpoint · send_gate ≠ 메일 캠페인 |

대형 클라우드 GraphRAG·Constitutional AI와 **같은 문제 정의**, **경량 스크립트·로컬 아티팩트**로 재현 가능성을 추적한다 (동급 제품 주장 아님).

---

## Universal Root PoC (Phase 15–17 · fixture bench · 2026-06-21)

**상태:** `[HYPO]` · `research_only` · **HF/Ollama 없이** Cursor·클론 환경에서 재현 가능한 OSS 스모크.

```powershell
py scripts/run_universal_root_oss_cursor_smoke_v1.py
```

| plane | metric | raw (fixture 500-pair) |
|-------|--------|------------------------|
| lexicon 41k | `prime_hit_rate` | **99.53%** |
| lexicon 41k | `english_only_distortion_rate` | **0.47%** |
| topology 31k | `verse_reachable_rate` | **99.53%** |
| walls | divergence exception cards | **2** (`heal`, `learn`) |

**격벽:** 위 수치는 **벤치 fixture 경로 raw** — repair uplift·Track A·실매매·투자 헤드라인 **합산 금지**. Gate spec phase **17** · `send_gate: HOLD`.

| 산출물 | 경로 |
|--------|------|
| OSS smoke | `reports/universal_root_oss_cursor_smoke_v1_latest.json` |
| Topology crosswalk | `reports/universal_root_topology_crosswalk_v1_latest.json` |
| Wall exceptions | `docs/final/artifacts/UNIVERSAL_ROOT_WALL_DIVERGENCE_EXCEPTION_CARDS_V1.json` |
| GATE_SPEC | `docs/final/artifacts/UNIVERSAL_ROOT_GATE_SPEC_V1.json` |

---

## Integrity Pipeline 레퍼런스 (성경 레일 · 부록만)

**포지션:** 성경 데이터 **판매 SKU 아님** — Fact-Lock·격벽·대기열이 어떻게 동작하는지 보여 주는 **극단적 레퍼런스 구현체**. 압축 B2B(§3.1) 무결성 스토리의 **뒷받침 증거**로만 사용.

| 케이스 | CROSS_REF | 상태 | 상용 메시지 (구조만) |
|--------|-----------|------|----------------------|
| **ENTRY_13** | 벤치 `Ps.5.2` · shadow `Ps.5.8-9` on 4Q98b | `commander_verified_shadow_witness` · **`verified_anchor` 미달** | 앵커 없는 MT v.2 직접행 주장 **금지** — 섀도우는 **라벨 분리** |
| **ENTRY_16** | `Ezra.2.54` · 4Q117 extant 범위 외 | `missing_anchor_until_source_update` · waiting queue 8단계 | 증거 부족 시 **폐기하지 않고 대기열** — `missing_anchor` 정직 표기 |

**재현 (내부·인바운드 부록):**

```powershell
py scripts/run_entry_13_16_deep_research_supplement_chain_v1.py
```

| 산출물 | 경로 |
|--------|------|
| ENTRY_13 shadow supplement | `reports/deep_research_entry_13_ps5_8_9_shadow_supplement_v1_latest.json` |
| ENTRY_16 Ezra plan | `reports/deep_research_entry_16_ezra_2_54_waiting_queue_plan_v1_latest.json` |
| 성경 레일 standby | CENTRAL checkpoint · `verified_anchor_achieved: false` · CROSS_REF 무변경 |

**쇼룸 데모 (Integrity Orb · Tier 3 · artifact-bound):**

| 항목 | 값 |
|------|-----|
| URL (배포 후) | `https://api.jemaai.cloud/public_showroom_logos_integrity_orb_v1.html?product=1` |
| 로컬 HTML | `projects/bitcoin-trading/ops/windows-rehearsal/jemaai-cloud-mvp/public_showroom_logos_integrity_orb_v1.html` |
| 슬라이스 JSON | `showroom_logos_integrity_orb_slice_v1.json` (ENTRY_13/16 · 15 nodes · 2 presets) |
| 재현 | `py scripts/build_showroom_logos_integrity_orb_slice_v1.py` · 번들 9/9: `build_showroom_track_c_bundle_chain_v1.ps1` |

→ no live LLM · gap 표시 when `verified_anchor: 0` · 압축 KPI 헤드라인 **합산 금지**

**쇼룸 데모 (Research Shadow Lane · Boundary + 가설 경로 · Tier 3):**

| 항목 | 값 |
|------|-----|
| 질의 예시 | 「욥이 고난을 받은 이유」— **인과 단정 없음** · 본문 lookup + 가설 트리 + 라우터 miss 관측 |
| URL (배포 후) | `https://api.jemaai.cloud/public_showroom_research_shadow_lane_v1.html` |
| 슬라이스 JSON | `showroom_research_shadow_lane_v1.json` (7 hypotheses · 3색 태그 · HITL) |
| 재현 | `powershell -File scripts/run_hypo_generation_chain_v1.ps1 -IssueId job_prologue_suffering` |

→ Structured boundary: corpus는 보여주되 **최종 판단은 지휘관** · DSS/외경은 `in_repo: false`면 literature pointer만

---

## 레인별 게이트 상태 (대외 자료 필수 표)

| 레인 | 제품/역할 | `send_gate` | 대외 헤드라인 합산 |
|------|-----------|-------------|-------------------|
| 압축 B2B | §3.1 1차 매출 | 인바운드·절차별 SSOT | **본선 KPI** (FAIL-COMP-004 분리 유지) |
| Logos Neuro-Symbolic | §3.1.8 부록·검증 배관 | **HOLD** | 압축 %·토큰 수와 **합치지 않음** |
| 성경 CROSS_REF 레일 | Integrity 레퍼런스 | **HOLD** | 학술 주석·B2C SKU **아님** (Tier 2/3 HOLD) |

---

## B2B 적용 시나리오 (구조 이식만)

1. **Ψ Logic Extraction** — 제안서 고유명사를 `Actor_A / Constraint_B` 등 **역할 노드**로만 추상화 (theology token filter)
2. **3단계 결정론 체인** — Alpha(제약·우회) / Beta(동시성) / dialectical resolution + **보정 노드**
3. **경로 검증 V(Sᵢ)** — 문장별 인용·그래프 경로 일치 여부 스코어링
4. **완성도 hot-reload** — 실행 → 9항목 점수 → 미달 시 자동 보정 루프 (target ≥90)

---

## Fact-Lock 근거 (내부·재현)

```powershell
py scripts/run_logos_track_b_hot_reload_v1.py --verbose
py scripts/build_logos_phase_o_completion_gate_v1.py
```

| 산출물 | 경로 |
|--------|------|
| 운영자 보드 | `reports/logos_hot_reload_operator_board_v1_latest.md` |
| Phase O digest | `reports/logos_phase_o_digest_v1_latest.md` |
| Completion gate | `reports/logos_phase_o_completion_gate_v1_latest.json` |
| B2B mapping (7/7 structure) | `reports/logos_b2b_logic_mapping_audit_v1_latest.json` |

**격벽:** `track_a_bridge: false` · `live_trading_bridge: false` · `theology_to_sales_forbidden: true`

---

## GTM 포지션 (Track C)

- **본선:** §3.1 GitHub·a-codeai 오픈벤치 (1인 개발자 GTM) — **§3.1.7**
- **본 절:** B2B **인바운드 부록**·데크·파일럿 설명용 — MS 헤드라인에 **로고스 수치 합산 금지**
- **쇼룸:** api.jemaai.cloud — `[NON_GATING]` 데모만; 자동 트리거 아님 · **Integrity Orb** (`https://api.jemaai.cloud/public_showroom_logos_integrity_orb_v1.html?product=1`) = ENTRY_13/16 Fact-Lock 시각화

---

*개정: 2026-06-21 · Universal Root Phase 15–17 fixture OSS smoke + dual-plane raw metrics*

---

## Audit smoke pointer (auto)

Latest B2B sales one-pager: `docs\final\artifacts\logos_rag_integrity_audit_one_pager_b2b_v1_latest.md`
Smoke artifact: `docs\final\artifacts\compression_open_bench_logos_audit_smoke_v1_latest.json`
