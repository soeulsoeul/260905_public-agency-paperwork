# 공공기관 부서장 업무효율화 멀티에이전트 — Claude Code 템플릿

이 문서 세트는 Claude Code를 업무 보조 환경으로 사용할 때, 부서장 승인 아래 문서 작성·현황 분석·규정 검토·공공데이터 조사를 분담시키기 위한 시작점이다.

## 적용 순서

1. 이 폴더의 `CLAUDE.md`를 대상 저장소 최상위에 복사한다.
2. `.claude/agents/`의 역할 파일을 대상 저장소의 같은 경로에 복사한다.
3. `.claude/skills/`의 메타 스킬(`blueprint`, `deep-dive`, `autoresearch`, `reflect`)을 같은 경로에 복사한다. 새 하위 에이전트·업무 흐름을 설계·개선할 때 사용한다.
4. `docs/`의 정책 파일을 내부 규정, 보유 시스템, 위임 전결 기준에 맞게 확정한다.
5. 운영 시작 전 `docs/approval-policy.md`의 승인 대상과 `docs/security-policy.md`의 데이터 등급을 기관 정보보호 담당자와 검토한다.

## 구성

| 파일 | 용도 |
| --- | --- |
| `CLAUDE.md` | 모든 Claude Code 작업에 적용할 총괄 운영 원칙 |
| `.claude/agents/*.md` | 업무별 전문 하위 에이전트의 역할·산출물·금지사항 |
| `.claude/skills/*` | 에이전트 체계 설계·보강·개선·마무리용 메타 스킬 (아래 표) |
| `docs/agent-problem-definition-template.md` | `blueprint` 사용 전 문제·범위·성공기준을 정리하는 템플릿 |
| `docs/prompt-learning-sdk-setup.md` | (선택) 자연어 피드백 기반 프롬프트 자동 개정 SDK 설치·승인 절차 |
| `docs/approval-policy.md` | 사람 승인과 전결 기준 |
| `docs/security-policy.md` | 개인정보·비공개 정보·외부 도구 보안 기준 |
| `docs/official-document-style-guide.md` | 개조식 공문서 문체와 편집 기준 |
| `docs/workflow-catalog.md` | 요청부터 결과 검토까지의 표준 흐름 |
| `docs/operational-runbook.md` | 운영, 기록, 장애·오류 대응 기준 |
| `documents/YYMMDD_<주제>/` | `document-drafter`가 작성한 문서 산출물을 주제별로 모아 두는 폴더. `YYMMDD`는 해당 주제 폴더 최초 생성일 (`CLAUDE.md`의 "산출물 저장 위치" 참조) |

## 메타 스킬 (`.claude/skills/`)

민원·정책 산출물이 아니라 이 에이전트 체계 자체를 설계·개선하기 위한 도구다. 새 하위 에이전트나 업무 흐름을 추가할 때 다음 순서로 사용한다.

```
docs/agent-problem-definition-template.md 작성 → blueprint → deep-dive → (구현) → autoresearch → reflect
```

| 스킬 | 역할 |
| --- | --- |
| `blueprint` | 새 하위 에이전트/업무 자동화의 설계 문서 작성 (구조 검증 스크립트 포함) |
| `deep-dive` | 다단계 인터뷰로 설계 문서의 빈틈·암묵 전제를 보강 |
| `autoresearch` | 스킬·에이전트 프롬프트를 반복 실행·평가해 자동 개선 (실제 개인정보·비공개 자료 사용 금지) |
| `reflect` | 세션 마무리 시 학습·후속 조치를 `docs/solutions/`에 기록 (`CLAUDE.md`·`.claude/agents/*.md`는 수정하지 않음) |

이진 평가 기준이 없고 검토자의 자연어 코멘트만 있을 때는 `autoresearch/references/prompt-learning-guide.md`의 자연어 피드백 개선 절차를 먼저 적용한다. 대량 피드백을 외부 SDK로 자동 처리하려면 `docs/prompt-learning-sdk-setup.md`의 승인 절차를 거친다.

출처: [byungjunjang/jangpm-meta-skills](https://github.com/byungjunjang/jangpm-meta-skills), [Arize-ai/prompt-learning](https://github.com/Arize-ai/prompt-learning)

## 원칙

- 에이전트는 초안을 만들고, 책임 있는 공무원이 검토·결정·발송한다.
- 외부 시스템 쓰기, 대외 발송, 결재 상신, 원본 데이터 변경은 반드시 승인 후 실행한다.
- 개인·민감·비공개 정보는 필요한 최소량만 사용하며, 외부 모델 또는 MCP 서버로 보내기 전에 등급과 반출 가능 여부를 확인한다.
- 사실·법령·통계 수치는 근거 링크, 기준일, 불확실성을 함께 제시한다.

> 이 템플릿은 법률 자문이나 기관 보안정책을 대체하지 않는다. 실제 적용 전 기관의 개인정보·기록물·정보보안·전결 규정을 우선 적용한다.
