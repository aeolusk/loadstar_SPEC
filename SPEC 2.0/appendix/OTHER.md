# 부록 — Other (OTHER)

> 공통 규칙은 `02.ELEMENT_FORMAT.md` 참조.

## 목적

`02.ELEMENT_FORMAT.md` §1의 "형식 없는 일반 파일" 중, GROUP으로 조직화하고 싶은 것들을 위한 예외적 FORMAT. GROUP의 ITEMS에 참조되려면 카탈로그에 속한 FORMAT이어야 하는데(§4 참조 방식), OTHER는 그 최소 요건만 채워주는 자리다.

## 명명 규칙 — 유일한 예외

다른 모든 FORMAT과 달리 `[FORMAT][VER][DATE]이름.md` 구조화된 이름을 요구하지 않는다. `.loadstar/OTHER/` 아래 있으면 그것만으로 OTHER로 인식한다 — 자유 파일명 허용.

같은 폴더 내 파일명이 겹치지 않아야 하는 것(§5 동명 충돌)은 다른 FORMAT과 동일하게 적용된다.

참조 시 이름만으로 FORMAT을 구분한다: 참조된 파일명이 `[FORMAT][VER][DATE]이름.md` 패턴에 맞지 않으면 OTHER로 간주하고 `.loadstar/OTHER/`에서 찾는다(§4).

## 고유 슬롯

없음. 공통 봉투(§6의 IDENTITY/CONNECTIONS)도 요구하지 않는다 — 내용은 완전히 자유 형식이다.

## 구조 추출기와의 관계

구조 추출기(①)는 OTHER 파일의 내부 구조를 파싱하지 않는다(파싱할 구조가 없음) — 파일 존재와 GROUP 소속 여부만 nodes/edges에 반영한다.
