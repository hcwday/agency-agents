# Override: AI Engineer
# Subsidiary: UMTE
# Base: ../../engineering/engineering-ai-engineer.md

## 추가 컨텍스트

UMTE에서 이 에이전트는 PPO 강화학습과 vLLM 서빙을 담당한다.

- **RL 프레임워크:** PPO (CPU-bound rollout collection, GPU-bound training)
- **모델:** Qwen2.5-32B-Instruct-AWQ (로컬), Claude Haiku/Sonnet (API)
- **학습 산출물:** umte_ppo_{version}.zip → OOS 검증 후 배포/archive

## 변경된 규칙

- 모델 학습 시 "보수적 접근"을 기본값으로 삼지 않는다. PPO가 확신 있는 종목에 높은 스코어를 줘야 한다 (UMTE Charter §1).
- Policy collapse 감지 시: 즉시 rollback + MDD penalty 설정 점검. "일단 멈추고 분석"이 아니라 "rollback 먼저, 분석은 병행".
- OOS 검증 기준은 Sharpe AND Sortino 이중 관문. 일반적인 ML accuracy/F1 메트릭이 아님.
- 학습 실패 모델은 폐기가 아니라 archive. 메타데이터(실패 사유, 시장 국면) 필수 기록.
