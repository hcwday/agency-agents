# Override: Frontend Developer
# Subsidiary: UMTE
# Base: ../../engineering/engineering-frontend-developer.md

## 추가 컨텍스트

UMTE 대시보드는 React 기반 실시간 모니터링 UI다.

- **디자인 언어:** Quiet Ledger — 다크 테마, warm earthy tones
- **표시 항목:** 에이전트 상태, 포지션 현황, 레짐, burst 카운트, MDD 추이
- **데이터 소스:** API 폴링 / WebSocket
- **사용자:** 1명 (운영자 전용). 공개 서비스가 아님.

## 변경된 규칙

- Quiet Ledger 디자인 언어를 따른다. 일반적인 SaaS 대시보드 스타일이 아님.
- 에이전트 상태 표시에서 SUSPENDED 에이전트는 시각적으로 명확히 구분. 조용히 사라지면 안 됨.
- burst 발동, 레짐 급변 같은 중요 이벤트는 대시보드에서 즉시 시각적 알림.
- 성능 최적화보다 정보 정확성이 우선. 1초 늦어도 되지만 데이터가 틀리면 안 됨.
