# 선택 도구: Arize prompt-learning SDK/CLI 설치 안내

출처: [Arize-ai/prompt-learning](https://github.com/Arize-ai/prompt-learning) (Elastic License 2.0). 자연어 피드백으로 프롬프트를 자동 개정하는 Python SDK/CLI다.

이 도구는 본 템플릿의 기본 구성이 아니며 선택 사항이다. 세션 내에서 사람이 직접 규칙을 반영하는 방법은 `.claude/skills/autoresearch/references/prompt-learning-guide.md`를 우선 사용하고, 이 SDK는 대량의 피드백 데이터셋을 자동으로 반복 처리해야 할 때에만 검토한다.

## 적용 전 확인 (필수)

- 이 SDK는 프롬프트·데이터셋을 OpenAI 또는 Google AI API로 전송한다. `docs/security-policy.md`의 "개인정보·민감정보 외부 전송" 및 `docs/approval-policy.md`의 "개인정보·비공개 정보 반출" 항목에 해당하므로, 사용 전 정보보호 담당자 승인을 받는다.
- 데이터셋(`input/output/feedback` 열)에는 실제 민원인·주민 개인정보, 비공개 인사·감사 자료를 넣지 않는다. 가상 사례 또는 비식별화된 예시만 사용한다.
- API 키는 문서·코드·프롬프트에 직접 기재하지 않고, 기관이 승인한 비밀관리 방식(환경변수, 시크릿 매니저 등)으로 주입한다.
- 실행마다 비용이 발생하므로 `--budget` 상한을 반드시 지정하고, 소액으로 먼저 검증한다.

## 설치

```bash
git clone https://github.com/Arize-ai/prompt-learning.git
cd prompt-learning
pip install -e .
```

## 환경변수

```bash
# OpenAI 사용 시
export OPENAI_API_KEY="<기관 승인 절차로 발급받은 키>"

# 또는 Google AI/Gemini 사용 시
export GOOGLE_API_KEY="<기관 승인 절차로 발급받은 키>"
```

## 기본 사용 예 (CLI)

```bash
prompt-learn optimize \
  --prompt "$(cat .claude/agents/document-drafter.md)" \
  --dataset feedback-dataset.csv \
  --output-column draft \
  --feedback-columns reviewer_feedback \
  --budget 5.00 \
  --save optimized-document-drafter.md
```

- `feedback-dataset.csv`는 최소 `draft`(하위 에이전트 산출물)와 `reviewer_feedback`(검토자의 자연어 코멘트) 열을 포함해야 한다. 실제 민원 원문 대신 요약·비식별화된 사례를 넣는다.
- `--save`로 저장한 결과는 바로 `.claude/agents/`에 덮어쓰지 않는다. 담당자가 기존 규칙과 비교·검토한 뒤 필요한 부분만 `Edit`로 반영한다.

## 결과 반영 절차

1. `--save`로 저장된 초안 프롬프트를 사람이 검토한다.
2. 기존 `.claude/agents/<name>.md`의 안전 규칙·승인 문구·문체 기준(`docs/official-document-style-guide.md`)이 그대로 유지되는지 확인한다. SDK는 이 문서 세트를 모르므로 자동 반영된 문장이 상충할 수 있다.
3. 승인된 변경만 `.claude/agents/<name>.md`에 반영하고, 변경 사유와 근거 피드백을 커밋 메시지 또는 운영 기록에 남긴다(`docs/operational-runbook.md`의 기록 기준 준수).
