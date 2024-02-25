```mermaid
flowchart LR

Home[화면]
Sidebar[사이드바]
Header(헤더)
Footer(푸터)
List(글 목록)

Home --- Header

Home --- Footer

Home --- Sidebar

Home --- List


Create[글 작성화면]
Admin[관리자 화면]
ChatGpt[Ai 섹션]
Detail[상세]


TagList[태그 목록 화면]
Tag[태그 화면]
Category[카테고리 화면]

Header -.-> ChatGpt

Sidebar -.-> TagList

Sidebar -.-> Category

Footer -.-> Create

Footer -.-> Admin

List -.->Detail

TagList -.-> Detail


```

[] 화면 () 구성요소
