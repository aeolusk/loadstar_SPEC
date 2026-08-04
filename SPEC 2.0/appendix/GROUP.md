# 부록 — Group (GROUP)

> 공통 규칙은 `02.ELEMENT_FORMAT.md` 참조.

## 목적

WP·DWP·OTHER·다른 GROUP을 조직화하기 위한 순수 카테고리 컨테이너. **선택적이다** — 모든 WP가 GROUP에 속할 필요는 없다. 큰 프로젝트에서 TODO·작업 현황을 하나의 거대한 단위로 관리하기엔 복잡도가 너무 높아질 때, 자연스럽게 분산 관리할 수 있는 선택지를 열어두는 용도다.

## 고유 슬롯

| 슬롯 | 값 | 비고 |
|:--|:--|:--|
| `CONNECTIONS.ITEMS` | WP/DWP/OTHER/하위 GROUP 파일명 리스트 | 이 GROUP이 논리적으로 묶는 대상 |

STATUS·GOAL·TODO·TABLES는 갖지 않는다.

## 멤버십 방향 — 반드시 지켜야 하는 원칙

**GROUP만 멤버를 안다. WP/DWP는 자신이 어느 GROUP에 속하는지 전혀 모른다.** WP/DWP의 `CONNECTIONS`에는 GROUP 관련 정보를 절대 기술하지 않는다 — GROUP은 순수하게 논리적 관리만 담당하고, WP/DWP는 조직화 구조를 몰라도 되는 상태를 유지한다.

- 소속 편입·해제는 오직 GROUP 파일의 `ITEMS`를 고치는 것으로만 이뤄진다.
- **알려진 트레이드오프**: 새 WP를 만들고 어느 GROUP에도 등록하지 않으면 그 WP는 논리적으로 "미분류" 상태로 조용히 남는다 — 이건 깨진 참조(dangling reference)와 달리 검증기가 기계적으로 잡아내기 어렵다(WP가 어떤 GROUP에 속해야 "마땅한지"는 사람의 의도이기 때문). 이 트레이드오프는 의도적으로 감수한다.

## 중첩

GROUP의 `ITEMS`에 다른 GROUP 파일명을 넣으면 그 GROUP이 하위로 중첩된다(대분류 GROUP의 ITEMS에 중분류 GROUP들을 나열하는 식). 몇 단계까지 중첩할지는 자유다.

## 포맷

```
### IDENTITY
- SUMMARY: 이 그룹이 묶는 대상이 무엇인가

### CONNECTIONS
- ITEMS: WP/DWP/OTHER/하위 GROUP 파일명 리스트

### COMMENT (선택)
- 자유 형식 코멘트
```
