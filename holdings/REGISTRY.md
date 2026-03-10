# Subsidiary Registry

| # | Name | Status | 에이전트 수 | 편입일 | 비고 |
|---|------|--------|-----------|--------|------|
| 1 | UMTE | `active` | 20 (자체) + 3 (공유) | 2025-03-09 | Ultra Multi-layered Trading Engine |
| 2 | Quiet Ink | `planned` | — | — | 콘텐츠 퍼블리싱 파이프라인 |
| 3 | Madang (마당) | `planned` | — | — | 한인 스몰비즈 마케팅 |

---

## UMTE — Active

**미션:** 자율 트레이딩 시스템  
**운영 철학:** 겁쟁이 금지 / 자율 감시 + 선제 행동  
**인프라:** DGX Spark (GB10) + Claude API (Haiku/Sonnet)  
**스킬 경로:** `subsidiaries/umte/SKILL.md`

### 공유 서비스 사용 현황

| 공유 에이전트 | 용도 | Override |
|-------------|------|---------|
| `engineering-devops-automator` | nightly pipeline, DGX Spark CI | `devops-automator.override.md` |
| `engineering-ai-engineer` | PPO 학습, vLLM 서빙 | `ai-engineer.override.md` |
| `testing-performance-benchmarker` | OOS 검증, Sharpe/Sortino 벤치마크 | `performance-benchmarker.override.md` |

---

## Quiet Ink — Planned

**미션:** 한국어 시장분석 칼럼 자동 발행  
**운영 철학:** 사람이 쓴 것처럼 / SEO는 수단이지 목적이 아님  
**인프라:** Pipedream + WordPress  
**예상 에이전트:** IR-Communicator (UMTE에서 이관), SEO Optimizer, Editorial Voice, Publish Scheduler, Content Auditor

---

## Madang (마당) — Planned

**미션:** 한인 소규모 사업자 디지털 마케팅 지원  
**운영 철학:** 진정성 > 퍼포먼스 / 동네 신뢰 우선  
**인프라:** Social platforms + Google Business Profile  
**예상 에이전트:** Local SEO Specialist, Korean Community Manager, Google Business Optimizer + 공유풀 차용 (Content Creator, Instagram Curator, Analytics Reporter)
