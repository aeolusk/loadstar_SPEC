# 부록 — Data WayPoint (DWP)

> 공통 규칙은 `02.ELEMENT_FORMAT.md` 참조.

## 목적

데이터의 개념적 자기소개. 작업 단위가 아니므로 TODO·GOAL을 갖지 않는다.

## 고유 슬롯

| 슬롯 | 값 | 비고 |
|:--|:--|:--|
| `TABLES` | 카테고리 → 테이블 → 요소 3단 구조 (선택) | 단순한 DWP는 SUMMARY만으로 충분할 수 있다 |

## 포맷

```
### IDENTITY
- SUMMARY: 이 데이터가 개념적으로 무엇인가 (자기소개)

### CONNECTIONS
- PARENT: 상위 요소 파일명 (없으면 이 줄 자체를 생략). GROUP은 여기 기술하지 않는다 — 소속은 GROUP 쪽에서만 관리(`appendix/GROUP.md`).
- REFERENCE: 참조 관계 파일명 리스트

### TABLES (선택)
- 테이블명1:
  - 요소
  - 요소: 한 줄 설명 (선택)

### ATTACHMENTS (선택)
- file:///backend/db/migrations/V12__create_users.sql

### ISSUE (없으면 생략 가능)
- 설계 시점 알려진 제약/미결 문제

### COMMENT (없으면 생략 가능)
- 자유 형식 코멘트
```

## 작성 원칙

- **추상 우선**: ERD/DDL 수준의 구체 스펙은 DWP의 영역이 아니다.
- **요소 슬롯 금지 사항**: 타입/제약/인덱스/외래키 등 구체 스펙은 적지 않는다. 정확한 스펙 위치는 `ATTACHMENTS`로 안내한다(CODE_MAP 제거 — 재검토 예정, `02.ELEMENT_FORMAT.md` 참조).
- **요소 표기**: `이름` 또는 `이름: 한 줄 설명`까지만 적는다.
- **관계는 작업 측에서 발생한다**: DWP 간 관계는 그 데이터를 다루는 WP의 작업 기록에서 자연스럽게 드러나게 한다.
- **TODO/GOAL을 갖지 않는다**: DWP 정의 변경은 그 DWP를 다루는 WP의 TODO에 항목으로 등록한다.
