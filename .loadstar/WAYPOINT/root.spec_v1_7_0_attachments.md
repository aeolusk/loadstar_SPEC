<WAYPOINT>
## [ADDRESS] W://root/spec_v1_7_0_attachments
## [STATUS] S_STB

### IDENTITY
- SUMMARY: SPEC v1.6.0 → v1.7.0 — WP/dwp에 `ATTACHMENTS` 슬롯 신설. URL 스킴(`https://`, `file:///`) 기반으로 LOADSTAR 그래프 외부 자료(SQL, 설계 문서, 외부 URL 등)를 1급으로 매단다. 검증 룰은 본 WP 범위 밖.
- METADATA: [Priority: P1, Created: 2026-05-12]
- SYNCED_AT: 2026-05-12

### GOAL
LOADSTAR가 다루는 자료의 경계를 그래프 내부(`M://`, `W://`, `D://`) 너머의 외부 파일·URL까지 확장한다. dwp가 "구체 스펙 금지" 원칙을 유지하면서도 SQL/DDL 같은 정확한 스펙 파일에 도달할 수 있는 표준 자리를 갖고, WP는 작업 참고 자료(설계 PDF, 회의록, 마이그레이션 스크립트 등)를 코드 그래프와 분리해 매달 수 있다. 표기는 표준 URL 스킴을 차용해 향후 별도 처리(브라우저 오픈, 파일 미리보기, 외부 인덱서 연동 등)를 단일 규약으로 흡수한다.

### CONNECTIONS
- PARENT: M://root
- CHILDREN: []
- REFERENCE: [W://root/spec_v1_6_0_goal_slot]

### CODE_MAP
- scope:
  - ./

### TODO
# TASK — SPEC 본문 패치
- [x] 2026-05-12 02.SCHEMA_DEF.md — §7 신설: Attachment URL Schemes (https / file 규약, 프로젝트 루트 기준 상대경로 정의)
- [x] 2026-05-12 05.ELEMENT_FORMAT.md — Map/WP/dwp 역할 비교표에 ATTACHMENTS 행 추가
- [x] 2026-05-12 05.ELEMENT_FORMAT.md — WP 포맷에 `### ATTACHMENTS` 섹션 신설 (CODE_MAP 직후, TODO 앞), 선택 항목 명시
- [x] 2026-05-12 05.ELEMENT_FORMAT.md — dwp 포맷에 `### ATTACHMENTS` 섹션 신설 (CODE_MAP 직후, ISSUE 앞), 선택 항목 명시
- [x] 2026-05-12 05.ELEMENT_FORMAT.md — ATTACHMENTS 표기 규약 추가 (URL 한 줄 또는 `URL — 설명`)

# TASK — 예시 / 메타데이터
- [x] 2026-05-12 examples/WP_TEMPLATE.md — ATTACHMENTS 섹션 예시 추가
- [x] 2026-05-12 examples/DWP_TEMPLATE.md — ATTACHMENTS 섹션 예시 추가
- [x] 2026-05-12 README.md / README.ko.md — v1.6.0 → v1.7.0, Document Index에 ATTACHMENTS 슬롯 반영
- [x] 2026-05-12 M://root에 본 WP 등록 + SYNCED_AT 갱신

# TASK — 검증
- [x] 2026-05-12 네 프로젝트 `loadstar validate` 통과 확인 — loadstar_SPEC (6 wp, 1 map), loadstar_cli (11 wp, 3 maps), loadstar_ui (38 wp, 5 maps), loadstar_mcp (1 wp, 1 map)

# RECURRING
- (R) SPEC 변경 후 README 버전 표기 동기화 확인
- (R) loadstar_SPEC / loadstar_cli / loadstar_ui / loadstar_mcp 네 프로젝트에서 `loadstar validate` 통과 확인

### ISSUE
- OPEN_QUESTIONS: []
- 본 WP는 표기 규격만. `loadstar validate`의 file://경로 존재 검증, https 도달성 검증 등은 후속 WP에서.
- file:// 경로 기준은 LOADSTAR 내부 재정의(프로젝트 루트 기준 상대경로). RFC 8089의 OS 절대경로 의미와는 다름 — SPEC에서 명시.
- 기존 WP/dwp 파일의 ATTACHMENTS 슬롯 추가는 점진 도입. 본 WP 범위 밖.

### COMMENT
- 표기 예:
  - `- https://example.com/spec.pdf`
  - `- file:///backend/db/migrations/V12__init.sql`
  - `- file:///docs/design/auth_flow.png — 인증 흐름 다이어그램`
- 호환성: ATTACHMENTS는 선택 항목이라 기존 모든 WP/dwp 파일 무수정 통과.
- 버전 정책: 호환 깨지지 않는 슬롯 신설 → minor bump (v1.6.0 → v1.7.0).
</WAYPOINT>
