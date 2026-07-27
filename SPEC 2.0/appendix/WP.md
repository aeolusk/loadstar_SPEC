# 부록 — WayPoint (WP)

> 공통 규칙은 `02.ELEMENT_FORMAT.md` 참조.

## 목적

모든 작업의 실행 단위. 하위 WayPoint를 가질 수 있다.

## 고유 슬롯

| 슬롯 | 값 | 비고 |
|:--|:--|:--|
| `STATUS` | `S_IDL` / `S_PRG` / `S_STB` / `S_ERR` / `S_REV` / `S_OOS` | 진행 상태의 단일 출처 |
| `GOAL` | 자유 텍스트 (선택) | 이 WP가 달성하려는 의도 |
| `TODO` | TASK/RECURRING 체크리스트 | 구체 작업 |
| `CONNECTIONS.CHILDREN` | 하위 WayPoint 파일명 리스트 | — |

### STATUS 코드

| 코드 | 의미 |
|:--|:--|
| `S_IDL` | Idle — 대기, 착수 전 |
| `S_PRG` | In Progress — 진행 중 |
| `S_STB` | Stable — 완료·안정 |
| `S_ERR` | Error — 오류 발생 |
| `S_REV` | Review Required — 검토 필요 |
| `S_OOS` | Out of Scope — 범위 제외(초기 계획에 있었으나 구현하지 않기로 확정) |

## SUMMARY · GOAL · TODO 의미 분담

| 슬롯 | 답하는 질문 |
|:--|:--|
| `SUMMARY` | 이게 무엇인가 (정체성) |
| `GOAL` | 이게 무엇을 달성하려 하는가 (의도) |
| `TODO` | 달성을 위한 구체 작업 |

WP 완료 시점에 TODO가 자기 GOAL을 충실히 실현했는지 사후 검토할 수 있다. GOAL이 길어지면 하위 WP로 분해하라는 신호다.

## 포맷

```
## [STATUS] 상태코드

### IDENTITY
- SUMMARY: 요소의 목적 및 정체성 요약

### GOAL (선택)
이 WayPoint가 달성하려는 의도. 한 문장~한 문단.
복수의 독립적 하위 목표는 번호 목록(G1. / G2. / ...) 허용.

### CONNECTIONS
- PARENT: 상위 WayPoint 파일명 (없으면 이 줄 자체를 생략 — 모든 WP가 상위를 가질 필요는 없다). GROUP은 여기 기술하지 않는다 — 소속은 GROUP 쪽에서만 관리(`appendix/GROUP.md`).
- CHILDREN: 하위 WayPoint 파일명 리스트
- REFERENCE: 참조 관계 파일명 리스트

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
- 설계 시점 알려진 제약/미결 문제나 미결정 사항을 자유 형식으로 기술한다.

### COMMENT
- 자유 형식 코멘트
```

## TASK 항목

- `- [ ]` 미완료 / `- [x] YYYY-MM-DD` 완료.
- AI 재진입 시 체크박스 상태로 "어디서 멈췄는가"를 즉시 파악한다.

## RECURRING 항목

- 표기: `- (R) 작업 설명`
- 코드가 바뀔 때마다 다시 수행해야 하는 작업(테스트/빌드/린트 등). TASK와 달리 완료 개념이 없다.
- 한 WP에 5개 이상 누적되면 스코프가 너무 넓거나 CI로 옮겨야 할 징후.

## TODO 아카이브 규칙 — ⚠️ 재검토 필요

완료 항목이 과다 누적되어 토큰 비용이 증가하면 완료 항목을 별도 파일로 분리할 수 있다는 것이 v1의 취지였다.

**미해결 문제**: `[FORMAT][VER][DATE]이름.md` 형식에서는 `이름`이 자유 텍스트라 `초기화 작업-archive-01` 같은 이름도 정상적인 WP로 파싱된다 — 즉 구조 추출기가 아카이브 파일을 일반 WP와 구분 없이 그대로 색인한다. v1에서는(우연히) 명명 규칙과 어긋나서 구조 추출기가 자동으로 걸러냈지만, 2.0에서는 그 성질이 사라졌다.

추가로, 이 규칙 자체의 존재 이유(토큰 비용 절감 — LLM 컨텍스트에 WP 전체를 로드하는 비용)가 2.0에서는 약해질 수 있다: AI가 SQLite(구조 추출기·온디맨드 조회기)를 거쳐 필요한 정보만 조회하는 방향이라면, WP 원본 파일 전체를 매번 컨텍스트에 로드할 필요 자체가 줄어든다. 다만 그 WP를 직접 편집(TODO 추가 등)할 때는 여전히 원본 파일을 열어야 하므로 완전히 무의미해지진 않는다.

**결정 보류** — 다음 중 하나로 정리 필요:
1. 아카이브를 별도 FORMAT(예: `WP_ARCHIVE`)으로 분리 — 명시적으로 카탈로그에 등록, 구조 추출기가 의도적으로 제외
2. 아카이브 규칙 자체를 폐기 — SQLite 조회 중심 워크플로우에서는 토큰 비용 절감 효과가 크지 않다고 보고 완료 항목을 그냥 WP 안에 계속 쌓는다
