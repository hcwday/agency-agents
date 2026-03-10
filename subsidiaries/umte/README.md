# UMTE — Ultra Multi-layered Trading Engine

**Status:** Active  
**편입일:** 2025-03-09  
**Parent:** The Agency Holdings

---

## 미션

자율 트레이딩 시스템. 20개 AI 에이전트가 3-Phase 파이프라인으로 시그널 생성 → 교차 검증 → 종합 실행을 수행한다.

## 운영 철학

두 원칙이 모든 설계 결정을 관통한다:

**겁쟁이 금지** — 방어만 하는 시스템은 죽은 시스템이다. Hard limit 안에서 공격적으로 행동한다. 기회를 놓치는 것도 리스크다.

**자율 감시 + 선제 행동** — 지시를 기다리지 않는다. 이상 발견 시 보고가 아니라 행동을 먼저 한다.

## 에이전트 구조

### Phase 1: Signal Generation

| Agent | 역할 | 모델 |
|-------|------|------|
| quant-alpha | 팩터 분석, composite score | sonnet |
| market-intel | 시장 전반 분석, 섹터 동향 | sonnet |
| intel-monitor | 실시간 뉴스/이벤트 감시 | haiku |
| data-validator | DQI 모니터링, silent degradation 탐지 | sonnet |
| ml-engineer | Farm System ML 모델 관리 | haiku |

### Phase 2: Cross-Validation

| Agent | 역할 | 모델 |
|-------|------|------|
| signal-validator | 시그널 신뢰도 판정 | haiku |
| risk-officer | 포지션 리스크, 스탑 근접, 레짐 위험도 | haiku |
| trade-sentinel | 매매 실행 감시, 체결 확인 | haiku |
| compliance | 규정 준수, 비정상 거래 패턴 감지 | haiku |

### Phase 3: Synthesis

| Agent | 역할 | 모델 |
|-------|------|------|
| ceo | 최종 의사결정, 종합 판단 | sonnet |
| cfo | 비용 분석, 세금, 효율성 | sonnet |
| baseball-report-stylist | 브리핑 변환 | haiku |
| + db-guardian, 팜 시스템 에이전트 등 | | |

### 공유 서비스 차용

| 공유 에이전트 | 원본 경로 | Override |
|-------------|----------|---------|
| DevOps Automator | `engineering/engineering-devops-automator.md` | DGX Spark 환경 특화 |
| AI Engineer | `engineering/engineering-ai-engineer.md` | PPO/vLLM 워크로드 특화 |
| Performance Benchmarker | `testing/testing-performance-benchmarker.md` | OOS Sharpe/Sortino 기준 적용 |

## 인프라

- **컴퓨트:** DGX Spark (GB10/Blackwell, hostname spark-f054)
- **LLM 서빙:** Qwen2.5-32B-Instruct-AWQ via vLLM (로컬) + Claude API Haiku/Sonnet (nightly pipeline)
- **자동화:** nightly_pipeline.py, weekly_audit.py
- **RL:** PPO 학습 (CPU-bound rollout → GPU training)

## 참조 문서

| 파일 | 내용 |
|------|------|
| `references/architecture.md` | 에이전트 구조, 팀 오케스트레이션, 성과 레지스트리 |
| `references/chandelier-director.md` | Optuna, Chandelier Exit, Director, Position Scaler |
| `references/operations.md` | Experience Bank, Fire Drill, 모니터링 |
| `SKILL.md` | Claude Code 스킬 (통합 reference) |
