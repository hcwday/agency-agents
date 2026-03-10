# Override: Performance Benchmarker
# Subsidiary: UMTE
# Base: ../../testing/testing-performance-benchmarker.md

## 추가 컨텍스트

UMTE에서 "성능"은 웹 로드 타임이 아니라 트레이딩 모델의 OOS(Out-of-Sample) 검증 결과다.

## 변경된 규칙

### 벤치마크 메트릭

| 메트릭 | 기준 | 비고 |
|--------|------|------|
| Sharpe Ratio | 현행 대비 상회 | 단독 통과 불가 |
| Sortino Ratio | 현행 대비 상회 | 단독 통과 불가 |
| MDD | 90일 롤링 기준 -7% 이내 | YTD 아님, 전기간 최고점 아님 |
| 거래 횟수 | 최소 5건/기간 | 미달 시 penalty |

### 합격 조건

Sharpe AND Sortino 모두 현행 대비 높아야 합격. 하나만 통과는 불합격.

### 실패 처리

- 실패 모델은 archive 저장 (폐기 아님)
- 실패 사유 메타데이터 필수 (Sharpe 미달? Sortino 미달? 둘 다?)
- 2주 재시도 금지 (과적합 방지)
- 축적된 실패 패턴 분석 → 학습 파이프라인 구조 개선 신호
