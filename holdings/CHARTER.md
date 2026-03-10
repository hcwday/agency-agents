# The Agency Holdings — Charter

이 문서는 홀딩 구조의 거버넌스를 정의한다.

---

## 구조 원칙

```
agency-agents/                    ← 기존 repo (shared services)
├── engineering/                  ← 공유 에이전트 풀
├── design/
├── marketing/
├── testing/
├── support/
├── ...                           ← 기존 Division 폴더 전부
│
├── holdings/                     ← NEW: 홀딩 거버넌스
│   ├── CHARTER.md               ← 이 파일
│   └── REGISTRY.md              ← subsidiary 목록 + 상태
│
└── subsidiaries/                 ← NEW: 자회사들
    ├── umte/
    ├── quiet-ink/               (planned)
    └── madang/                  (planned)
```

기존 Division 폴더들은 건드리지 않는다. upstream fork sync이 깨지면 안 되니까.
`holdings/`와 `subsidiaries/`만 추가한다.

---

## Shared Services 접근 규칙

### 누가 쓸 수 있나

모든 subsidiary는 기존 Division 에이전트를 자유롭게 참조할 수 있다.

```
# UMTE에서 DevOps Automator를 참조하는 예시
참조: ../engineering/engineering-devops-automator.md
오버라이드: subsidiaries/umte/shared-overrides/devops-automator.override.md
```

### Override 메커니즘

공유 에이전트를 subsidiary 맥락에 맞게 커스터마이징할 때:

1. 원본은 절대 수정하지 않는다 (upstream 보호)
2. `shared-overrides/` 폴더에 `.override.md` 파일을 만든다
3. Override 파일은 **추가 지시만** 담는다 (원본 교체가 아님)
4. 로딩 순서: 원본 먼저 → override 덧씌움

### Override 파일 포맷

```markdown
# Override: {agent-name}
# Subsidiary: {subsidiary-name}
# Base: ../{division}/{agent-file}.md

## 추가 컨텍스트
(subsidiary 특화 지시사항)

## 변경된 규칙
(원본 규칙 중 이 subsidiary에서 다르게 적용할 것)
```

---

## Subsidiary 편입 절차

### 신규 편입

1. `subsidiaries/{name}/` 디렉토리 생성
2. 필수 파일 작성:
   - `README.md` — 미션, 운영 철학, 에이전트 목록
   - `CHARTER.md` — 독립 거버넌스 규칙
   - `agents/` — 도메인 전용 에이전트들
3. `holdings/REGISTRY.md`에 등록
4. 공유 에이전트 사용 시 `shared-overrides/`에 override 작성

### 편입 조건

- 독자적인 운영 철학이 있을 것 (UMTE의 "겁쟁이 금지" 같은)
- 최소 3개 이상의 도메인 전용 에이전트가 있을 것
- 다른 subsidiary와 에이전트 역할이 겹치지 않을 것

### 해산/휴면

- `REGISTRY.md`에서 status를 `dormant`로 변경
- 에이전트 파일은 삭제하지 않음 (archive 유지)
- 공유 에이전트 override만 비활성화

---

## Claude Code 연동

### 스킬 파일 매핑

각 subsidiary의 `SKILL.md`는 Claude Code 스킬로 등록 가능:

```
~/.claude/skills/
├── umte-trading-optimization/
│   └── SKILL.md → subsidiaries/umte/SKILL.md
├── quiet-ink-publishing/
│   └── SKILL.md → subsidiaries/quiet-ink/SKILL.md
└── madang-marketing/
    └── SKILL.md → subsidiaries/madang/SKILL.md
```

### 에이전트 파일 매핑

```
~/.claude/agents/
├── (기존 agency-agents 에이전트들)
├── umte-*.md → subsidiaries/umte/agents/**/*.md
└── madang-*.md → subsidiaries/madang/agents/**/*.md
```

---

## 네이밍 컨벤션

| 레벨 | 패턴 | 예시 |
|------|------|------|
| 공유 에이전트 | `{division}-{role}.md` | `engineering-devops-automator.md` |
| Subsidiary 에이전트 | `{sub}-{role}.md` | `umte-quant-alpha.md` |
| Override | `{role}.override.md` | `devops-automator.override.md` |
| 스킬 파일 | `SKILL.md` | (각 subsidiary 루트) |
