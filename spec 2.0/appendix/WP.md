# 부록 — WayPoint (WP)

> 공통 규칙은 `05.ELEMENT_FORMAT.md` 참조.

## 목적

모든 작업의 실행 단위. 하위 WayPoint를 가질 수 있다.

## 고유 슬롯

| 슬롯 | 값 | 비고 |
|:--|:--|:--|
| `STATUS` | `S_IDL` / `S_PRG` / `S_STB` / `S_ERR` / `S_REV` / `S_OOS` | 진행 상태의 단일 출처 |
| `GOAL` | 자유 텍스트 (선택) | 이 WP가 달성하려는 의도 |
| `TODO` | TASK/RECURRING 체크리스트 | 구체 작업 |
| `CONNECTIONS.CHILDREN` | 하위 WayPoint 파일명 리스트 | — |

## SUMMARY · GOAL · TODO 의미 분담

| 슬롯 | 답하는 질문 |
|:--|:--|
| `SUMMARY` | 이게 무엇인가 (정체성) |
| `GOAL` | 이게 무엇을 달성하려 하는가 (의도) |
| `TODO` | 달성을 위한 구체 작업 |

WP 완료 시점에 TODO가 자기 GOAL을 충실히 실현했는지 사후 검토할 수 있다. GOAL이 길어지면 하위 WP로 분해하라는 신호다.

## 포맷

```
<WAYPOINT>
## [STATUS] 상태코드

### IDENTITY
- SUMMARY: 요소의 목적 및 정체성 요약
- SYNCED_AT: YYYY-MM-DD HH:mm (마지막으로 실제 상태와 동기화한 시각)

### GOAL (선택)
이 WayPoint가 달성하려는 의도. 한 문장~한 문단.
복수의 독립적 하위 목표는 번호 목록(G1. / G2. / ...) 허용.

### CONNECTIONS
- PARENT: 상위 요소 파일명 (최상위 WayPoint는 생략 가능)
- CHILDREN: 하위 WayPoint 파일명 리스트
- REFERENCE: 참조 관계 파일명 리스트

### CODE_MAP (선택 — 코드 수정이 수반되는 경우에만)
- scope: 탐색 범위 디렉토리 경로 (복수 가능)

### ATTACHMENTS (선택)
- https://example.com/spec.pdf
- file:///backend/db/migrations/V12__init.sql

### TODO
# TASK
- [ ] 미완료 항목
- [x] YYYY-MM-DD 완료된 항목

# RECURRING (반복 항목이 없으면 헤더째 생략 가능)
- (R) 변경 후 mvn test 실행

### ISSUE
- 설계 시점 알려진 제약/미결 문제
- OPEN_QUESTIONS:
  - `[Q1]` 미결
  - `[Q1 DEFERRED]` 보류
  - `[Q1 CONFIRMED] 인라인 요약` 확인 완료

### COMMENT
- 자유 형식 코멘트
</WAYPOINT>
```

## TASK 항목

- `- [ ]` 미완료 / `- [x] YYYY-MM-DD` 완료.
- AI 재진입 시 체크박스 상태로 "어디서 멈췄는가"를 즉시 파악한다.

## RECURRING 항목

- 표기: `- (R) 작업 설명`
- 코드가 바뀔 때마다 다시 수행해야 하는 작업(테스트/빌드/린트 등). TASK와 달리 완료 개념이 없다.
- 한 WP에 5개 이상 누적되면 스코프가 너무 넓거나 CI로 옮겨야 할 징후.

## TODO 아카이브 규칙

완료 항목이 과다 누적되어 토큰 비용이 증가하면 완료 항목을 별도 파일로 분리할 수 있다.

- **파일명**: `[WP][VER]이름[생성일]-archive-NN.md` (원본과 같은 폴더)
- **분리 시점**: S_STB 전환 시 또는 완료 항목 30개 이상 누적 시
- **내용**: 완료된 TODO TASK 항목만 (날짜 포함)
- **원본 WP COMMENT에 참조 기록**: `아카이브: [WP][2.0]초기화 작업[2026.07.25]-archive-01.md`
- 아카이브 파일은 일상 작업 시 로드하지 않는다.
