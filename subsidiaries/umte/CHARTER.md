# UMTE Charter — 독립 거버넌스

이 문서는 UMTE subsidiary의 독립 운영 규칙을 정의한다.
홀딩 CHARTER와 충돌 시 이 문서가 UMTE 도메인 내에서 우선한다.

---

## 절대 규칙

### 1. 겁쟁이 금지

- 최소 exposure ≥ 20%. 이 아래로 내려가는 파라미터는 버그.
- crisis 레짐에서도 exposure 0.4. 0이 아니다.
- Optuna objective에 "거래 5건 미만 penalty" 포함. 아무것도 안 하는 파라미터 걸러냄.
- +3%에서 전량 익절 금지. 단계별 profit taking (5%→10%→15%).

### 2. 자율 감시 + 선제 행동

- data-validator stale data 감지 → signal 생성 자동 중단 (승인 불필요)
- burst 발동 → Optuna 재최적화 자동 실행
- 레짐 급변 → Director exposure 즉시 조정
- 에이전트 품질 하락 → 레지스트리 자동 SUSPEND
- 보고서만 쌓이고 행동이 없으면 시스템 실패

### 3. Chandelier 불가침

PPO와 Director는 Chandelier 파라미터를 건드리지 않는다. Optuna만 레짐별로 최적화한다.

### 4. OOS 이중 관문

신규 모델은 Sharpe AND Sortino 모두 현행 대비 높아야 합격. 하나만 통과는 불합격.

---

## 공유 에이전트 사용 시 제약

UMTE가 홀딩 공유 에이전트를 차용할 때, 반드시 위 절대 규칙과 호환되어야 한다.

- DevOps Automator가 "안전을 위해 배포 중단"을 제안해도, 겁쟁이 금지 원칙에 따라 거래 자체를 멈추면 안 된다. 인프라 문제와 거래 중단은 별개.
- AI Engineer가 "모델 불확실하니 보수적으로"를 제안해도, PPO가 확신 있으면 밀어야 한다.
- Performance Benchmarker의 기준은 OOS Sharpe/Sortino이지, 일반적인 웹 성능 메트릭이 아니다.

---

## 에이전트 간 월권 금지

| Agent | 할 수 있는 것 | 할 수 없는 것 |
|-------|-------------|-------------|
| quant-alpha | 팩터 분석, 스코어 생성 | 리스크 판단, 매매 추천 |
| risk-officer | 리스크 평가, 경고 | 매수/매도 결정 |
| ceo | 최종 종합 판단 | 개별 팩터 가중치 직접 수정 |
| data-validator | 데이터 품질 판정, 시그널 중단 | 시그널 내용 수정 |
| trade-sentinel | 체결 감시, 불일치 탐지 | 주문 직접 생성 |

---

## 실행 순서 (변경 불가)

```
Optuna (Chandelier) → chandelier_config.json
  → Optuna (Director) → director_config.json
    → PPO 학습 (두 config 적용)
      → OOS 검증 (Sharpe AND Sortino)
        → 통과: 배포 / 실패: archive + 다음 달 재시도
```

이 순서를 뒤집거나 스킵하는 것은 어떤 상황에서도 허용하지 않는다.
