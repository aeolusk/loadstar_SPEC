<WAYPOINT>
## [ADDRESS] W://root/spec_v1_8_0_gd
## [STATUS] S_STB

### IDENTITY
- SUMMARY: SPEC v1.7.0 → v1.8.0 — `.loadstar/GD/` 슬롯 신설. 프로젝트 맥락을 Q&A 형태로 압축 유지하며, 점수 기반 decay/boost로 신선도를 자동 관리한다. AI가 세션 진입 시 참고하는 거친 맥락 요약본. (GD = Good Dopamin)
- METADATA: [Priority: P1, Created: 2026-06-01]
- SYNCED_AT: 2026-06-01

### GOAL
대규모 프로젝트에서 메타 정보가 폭발할 때 AI와 인간 모두 전체 맥락을 파악하기 어렵다. GD는 "지금 이 프로젝트에서 신경 써야 할 것들"을 용량 제한 있는 Q&A 목록으로 압축하고, CPU 스케줄링과 유사한 점수 정책으로 항목의 신선도를 자동 관리한다. AI가 세션 시작 시 이를 참고해 맥락을 빠르게 복원하는 것이 목표다.

### CONNECTIONS
- PARENT: M://root
- CHILDREN: []
- REFERENCE: [W://root/spec_v1_7_0_attachments]

### CODE_MAP
- scope:
  - ./

### TODO
# TASK — SPEC 본문 패치
- [x] 2026-06-01 02.SCHEMA_DEF.md — §8 신설: GD 슬롯 정의 (항목 스키마, 점수 정책, 파일 구조)
- [x] 2026-06-01 04.STORAGE.md — `.loadstar/GD/` 디렉토리 항목 추가
- [x] 2026-06-01 05.ELEMENT_FORMAT.md — GD 운영 규칙 섹션 추가 (세션 진입 시 참조 방법)
- [x] 2026-06-01 06.CLI_SPEC.md — `loadstar gd` 서브커맨드 명세 추가 (list / add / change / delete / tick / revive)

# TASK — 예시 / 메타데이터
- [x] 2026-06-01 README.md / README.ko.md — v1.7.0 → v1.8.0, Document Index에 GD 슬롯 반영
- [x] 2026-06-01 M://root에 본 WP 등록 + SYNCED_AT 갱신

# RECURRING
- (R) SPEC 변경 후 README 버전 표기 동기화 확인
- (R) loadstar_SPEC / loadstar_cli / loadstar_ui / loadstar_mcp 네 프로젝트에서 `loadstar validate` 통과 확인

### ISSUE
- OPEN_QUESTIONS: []
- GD 구현(loadstar_cli)은 본 WP 범위 밖 — SPEC 정의만.
- `loadstar gd tick` 호출 시점(세션 종료 hook vs 수동)은 CLI WP에서 결정.
- 점수 정책 파라미터(decay/boost/revival 값)는 본 버전에서 고정값으로 SPEC에 명시.

### COMMENT
- GD(Good Dopamin): 강화/망각 메커니즘을 도파민에 빗댄 이름. AI 대화 중 즉각 식별 가능하며, `GD-001` 형태 항목 ID로 참조된다.
- 변경 이력은 파일 내 보관하지 않고 git이 관리 — 파일은 현재 상태만 유지.
</WAYPOINT>
