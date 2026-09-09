# 표준 업무 흐름

## 1. 부서장 보고자료 작성

`요청 접수 → 자료 등급 확인 → document-drafter 초안 → policy-reviewer 근거 검토 → security-reviewer 반출 검토 → 부서장 검토 → 확정본 발송 승인`

필수 결과: 1쪽 요약, 본문, 근거 목록, 확인 필요 항목, 대외 발송 승인 여부.

## 2. 정책·사업 현황 분석

`질문 정의 → data-analyst 데이터 추출·분석 → policy-reviewer 제도 요건 확인 → security-reviewer 개인정보 검토 → 총괄 비교·요약 → 부서장 의사결정`

필수 결과: 지표 정의, 기준일, 분석 방법, 한계, 대안별 장단점.

## 3. 민원·대외 문의 회신 초안

`문의 분류 → 사실·규정 확인 → document-drafter 회신안 → security-reviewer 개인정보·표현 검토 → 책임자 승인 → 담당자가 발송`

에이전트는 민원인에게 직접 답변하거나 처리 결과를 확정하지 않는다.

## 4. 공공데이터 조사

`조사 목적 확인 → 공개 데이터만 탐색 → data-analyst 정리 → 출처·라이선스·기준일 검증 → 보고용 요약`

공개 데이터 API 키와 사용조건은 별도 관리하고, 에이전트에게 키 값을 노출하지 않는다.

## 5. 신규 하위 에이전트·업무 흐름 설계 (메타 스킬)

`docs/agent-problem-definition-template.md` 작성 → `blueprint` 설계 문서 작성 → `deep-dive` 보강 → 구현(에이전트/스킬 파일 작성) → `autoresearch` 반복 평가·개선 → 부서장 검토·승인 → `reflect` 세션 학습 기록

- 평가·개선 단계(`autoresearch`)에는 실제 개인정보·비공개 자료를 입력하지 않고 가상 또는 마스킹된 예시만 사용한다.
- 새 하위 에이전트를 실제 업무에 투입하기 전에는 본 지침의 승인·보안 정책(`docs/approval-policy.md`, `docs/security-policy.md`)에 따라 부서장·정보보호 담당자의 확인을 받는다.
