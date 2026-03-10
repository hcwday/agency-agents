# Override: Infrastructure Maintainer
# Subsidiary: UMTE
# Base: ../../support/support-infrastructure-maintainer.md

## 추가 컨텍스트

UMTE 인프라는 DGX Spark (GB10/Blackwell) 단일 머신에서 운영된다.

- **호스트:** spark-f054
- **GPU 워크로드:** vLLM (Qwen2.5-32B-Instruct-AWQ) + PPO 학습 (간헐적)
- **스케줄링:** nightly_pipeline.py (매일), weekly_audit.py (주간)
- **접속:** VS Code Remote SSH
- **클라우드 의존:** Claude API (외부), Pipedream webhook (외부)

## 변경된 규칙

- vLLM과 PPO 학습이 GPU를 경합한다. 동시 실행 시 OOM 가능. 스케줄링으로 분리하되, 학습이 nightly pipeline 시간에 겹치지 않도록.
- vLLM 서비스 다운 → Claude API fallback 자동 전환. 서비스 복구를 기다리며 파이프라인을 멈추지 않는다.
- 디스크 모니터링: signals.db, experience_bank.db, PPO 체크포인트(umte_ppo_*.zip)가 디스크를 채울 수 있음. archive 정책 필요.
- 네트워크 단절 시: 로컬 vLLM으로 최소 운영 가능해야 함. Claude API 의존 부분은 큐에 저장 → 복구 후 일괄 처리.
- 정전/재부팅 후: vLLM 서비스 자동 시작, nightly pipeline 스케줄러 자동 복구 확인.
