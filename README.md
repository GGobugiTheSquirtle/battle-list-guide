# 어나더에덴 배틀 리스트

게임 내 「배틀」 화면(개체 목록)을 번호순으로 정리한 페이지.

**→ https://ggobugithesquirtle.github.io/battle-list-guide/**

- **그리드** — 한 줄 3/4/5개 선택
- **한 장씩** — 순서대로 하나씩 (←/→ 키)
- **현황** — 0001~0534 번호판에서 미수집 번호 확인

---

## 제보 방법

번호판에서 비어 있는 번호를 찾아 스크린샷을 찍어 보내주세요.

1. 「배틀」 화면에서 해당 개체를 열고 **좌측 패널 전체**가 나오게 캡처
2. 정보창을 **아래로 스크롤해 「훈장 보상」까지** 보이게 한 장 더
   (이게 없으면 훈장 보상이 `미확인`으로 남습니다)
3. 「추가 정보」 버튼이 있으면 눌러서 한 장 더

**번호·이름·시작 조건은 화면에 다 찍혀 있어서 따로 적지 않아도 됩니다.** 스샷만 주시면 됩니다.

현재 미수집: 509 / 534. 훈장 보상 미확인: No.0480, 0488, 0489, 0533, 0534.
No.0488 화원의 왕은 일러스트 캡처가 없습니다.

---

## 데이터 갱신 (관리자)

데이터·이미지는 전부 스크린샷에서 생성됩니다. 손으로 JSON을 고치지 마세요.

```bash
# 1) 받은 스샷 더미를 판독용 contact sheet 로 정리
py -3.14 ../_tools/ingest_battlelist.py <제보_이미지_폴더>
#    → _tmp/battlelist_ingest/sheet_XX.jpg + manifest.tsv

# 2) sheet 를 보고 원본을 _archive/battle-list-screenshots/ 로 옮긴 뒤
#    ../_tools/build_battlelist.py 의 ENTRIES 에 행 추가

# 3) 이미지 크롭 + JSON 재생성
py -3.14 ../_tools/build_battlelist.py
```

`ENTRIES` 가 단일 진실원본이다. `data/battle_list.json` 과 `images/*.webp` 는 전부 생성물.

로컬 확인은 `py -3.14 -m http.server 8000` (fetch 때문에 `file://` 로는 안 열림).

---

## 구조

```
index.html                 단일 파일 SPA (CSS/JS 인라인)
data/battle_list.json      {max_no, entries[]} — 생성물
images/{id}.webp           일러스트 1100px
images/{id}_t.webp         썸네일 420px
images/{id}_info{n}.webp   「추가 정보」 팝업
```
