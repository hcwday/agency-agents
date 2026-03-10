# Override: Backend Architect
# Subsidiary: UMTE
# Base: ../../engineering/engineering-backend-architect.md

## 추가 컨텍스트

UMTE는 20개 AI 에이전트가 3-Phase 파이프라인으로 작동하는 트레이딩 시스템이다.

- **아키텍처:** prompt_loader.py → 팀 오케스트레이션 → 에이전트 호출 → 결과 합성
- **Phase 1:** Signal Generation (quant-alpha, market-intel, data-validator 등)
- **Phase 2:** Cross-Validation (signal-validator, risk-officer, trade-sentinel)
- **Phase 3:** Synthesis (ceo, cfo, baseball-report-stylist)
- **데이터 흐름:** 구조화된 JSON. 자연어 해석에 의존하지 않음.

## 변경된 규칙

- 리팩토링 시 에이전트 간 월권 구조가 깨지지 않는지 반드시 확인. quant-alpha가 리스크 판단 로직을 갖게 되면 아키텍처 위반이다.
- Phase 간 데이터 전달은 스키마 기반. 새 필드 추가 시 하위 호환성 유지.
- 에이전트 1개 실패 시 나머지로 계속 진행하는 fallback 패턴 유지. 전체 중단 구조를 제안하지 않는다 (UMTE Charter §1 겁쟁이 금지).
- DB 스키마 변경 시 signals.db, experience_bank.db 양쪽 마이그레이션 계획 필수.
- team_orchestrator.py가 시스템의 핵심 허브. 이 파일 수정은 항상 보수적으로.
