# 5장. CSS3로 배치, 리스트, 표, 폼, 애니메이션 꾸미기

## 강의 목표
1. CSS3로 HTML 태그가 출력되는 위치를 조절할 수 있다.
2. CSS3로 리스트를 예쁘게 꾸밀 수 있다.
3. CSS3로 표를 예쁘게 꾸밀 수 있다.
4. CSS3로 폼을 꾸미고 사용자의 입력에 반응하게 할 수 있다.
5. CSS3로 애니메이션, 전환(transition), 변환(transform) 효과를 만들 수 있다.

---

## 1. 배치

CSS3로 HTML 태그가 출력되는 위치를 지정하는 것. HTML 태그는 웹 페이지에 작성된 순서와 달리 배치할 수 있음.

### 배치 기능의 CSS3 프로퍼티들
`display`, `position`, `left/right/top/bottom`, `float`, `z-index`, `visibility`, `overflow`

---

## 2. 블록 박스와 인라인 박스

HTML 태그는 **인라인 태그**와 **블록 태그**로 나뉘며, 인라인 태그는 인라인 박스, 블록 태그는 블록 박스로 출력됨.

- **블록 박스**: 새 라인에서 시작하며, 왼쪽에서 오른쪽 끝까지 한 줄을 통째로 점유 (예: `<div>`)
- **인라인 박스**: 블록 안에 배치되며, 옆에 다른 태그를 함께 배치 가능 (예: `<span>`)

### 박스의 유형 제어: display

| 구분 | 블록 박스 (display:block) | 인라인 박스 (display:inline) | 인라인 블록 박스 (display:inline-block) |
|---|---|---|---|
| 줄바꿈 | 항상 새 라인에서 시작 | 새 라인에서 시작 못함, 라인 안에 있음 | 새 라인에서 시작 못함, 라인 안에 있음 |
| 배치 위치 | 블록 박스 내에만 배치 | 모든 박스 내 배치 가능 | 모든 박스 내 배치 가능 |
| 옆 요소 배치 | 불가능 | 가능 | 가능 |
| width/height | 크기 조절 가능 | 크기 조절 불가능 | 크기 조절 가능 |
| margin/padding/border | padding, border, margin 조절 가능 | margin-top, margin-bottom 조절 불가능 | padding, border, margin 조절 가능 |

- `display: block` 예: `<span>`을 block 박스로 지정하고 width·height를 100px, 60px로 지정하면 한 줄을 독점적으로 차지해 옆에 다른 태그가 배치되지 않음
- `display: inline` 예: `<div>`를 inline 박스로 지정하면 라인 안에서 다른 요소와 함께 배치되고, 공간이 좁으면 남은 부분이 다음 줄로 넘어감
- `display: inline-block` 예: inline-block 박스는 라인 안에 다른 요소들과 함께 배치되면서 동시에 width, height, margin으로 크기 조절도 가능

### 예제 5-1: display 프로퍼티로 박스 유형 설정
하나의 div 태그에 display 값을 none, inline, inline-block으로 각각 바꿔가며 보이기/숨기기와 배치 방식 차이를 비교하고, span 태그에 display:block을 적용해 인라인 요소를 블록으로 바꿔봄.

---

## 3. 박스의 배치: position

- **normal flow**: 웹 페이지에 나타난 순서대로 HTML 태그가 배치되는 기본 흐름
- `position` 프로퍼티로 normal flow를 무시하고 배치 가능

### position 프로퍼티를 이용한 배치 방법
| 배치 방법 | 값 |
|---|---|
| 정적 배치 (디폴트) | `position: static` |
| 상대 배치 | `position: relative` |
| 절대 배치 | `position: absolute` |
| 고정 배치 | `position: fixed` |
| 유동 배치 | `float: left` 또는 `float: right` |

- position을 사용할 때 태그의 위치는 `top`, `bottom`, `left`, `right` 프로퍼티로 지정하며, 배치 방법에 따라 의미가 다르게 사용됨

### 3-1. 상대 배치, position: relative
normal flow의 '기본 위치'에서 left, top, bottom, right 값만큼 이동한 '상대 위치'에 배치됨.

#### 예제 5-2: position:relative 상대 배치
5개의 div 중 h와 k 글자를 가진 2개의 div에 마우스를 올리면 각각 다른 방향으로 20px씩 상대 배치되는 모습을 보여줌.

### 3-2. 절대 배치, position: absolute
normal flow에서 완전히 빠져나와 지정한 left, top 위치에 고정되며, 브라우저 크기가 변해도 절대 배치된 태그의 위치는 변하지 않음.

#### 예제 5-3: position:absolute 절대 배치
크리스마스 트리 이미지 위에 여러 개의 p 태그(M, E, R, R, Y 글자)를 절대 배치로 흩뿌려 원하는 좌표에 고정시킴.

### 3-3. 고정 배치, position: fixed
브라우저 창을 기준으로 위치가 고정되어, 스크롤을 해도 화면의 같은 위치에 계속 출력됨.

#### 예제 5-4: position:fixed로 브라우저 하단 오른쪽에 고정 배치
크리스마스 트리 이미지와 함께 메시지 박스를 브라우저 하단 오른쪽에 항상 고정되도록 배치.

### 3-4. 유동 배치, float
문서 흐름에서 요소를 띄워 좌우 한쪽으로 모으고, 나머지 콘텐츠가 그 주위를 감싸며 흐르게 함.

#### 예제 5-5: float:right로 브라우저의 오른편에 항상 배치
공지사항 p 태그를 float:right로 지정해 화면 오른쪽에 고정시키고, 다른 텍스트가 그 옆으로 자연스럽게 흐르도록 함.

### 3-5. z-index
요소가 겹칠 때 위아래 쌓이는 순서(레이어 순서)를 지정. 값이 클수록 위쪽에 표시됨.

#### 예제 5-6: z-index로 카드 쌓기
스페이드 카드 4장을 절대 배치로 겹쳐놓고, z-index 값(-3, 2, 3, 7)에 따라 쌓이는 순서가 달라지는 것을 보여줌.

### 3-6. visibility
`visibility: hidden`으로 지정하면 요소가 차지하는 공간은 그대로 유지한 채 내용만 보이지 않게 됨(display:none과 달리 공간은 남음).

#### 예제 5-7: visibility로 텍스트 숨기기
리스트 문장 속 특정 단어(span)를 visibility:hidden으로 숨겨서, 빈칸은 남아있지만 글자는 보이지 않는 퀴즈 형태를 만듦.

### 3-7. overflow
박스 크기보다 콘텐츠가 넘칠 때 처리 방식을 지정. `hidden`(잘라서 숨김), `visible`(넘친 채로 출력), `scroll`(스크롤바 생성) 등의 값이 있음.

#### 예제 5-8: overflow 프로퍼티 활용
동일한 크기의 p 박스 3개에 각각 overflow:hidden, visible, scroll을 적용해 넘치는 텍스트가 어떻게 처리되는지 비교.

---

## 4. CSS3로 리스트 꾸미기

### 리스트의 모양을 꾸미는 CSS3 프로퍼티들

| 프로퍼티 | 설명 |
|---|---|
| list-style-type | 아이템 마커 타입 지정 |
| list-style-image | 아이템 마커 이미지 지정 |
| list-style-position | 아이템 마커의 출력 위치 지정(아이템 영역 내 혹은 영역 바깥) |
| list-style | 앞의 3개 프로퍼티 값을 한 번에 지정하는 단축 프로퍼티 |

### 리스트와 아이템에 배경색 입히기
`ul`에 background와 padding을 지정하고, `ul li`(자손 셀렉터)에 다시 background와 margin-bottom을 지정하여 리스트 전체와 각 아이템의 배경을 따로 꾸밀 수 있음. 마커는 기본적으로 아이템 바깥쪽(패딩 영역)에 위치함.

### 마커의 위치, list-style-position
`list-style-position: inside`로 지정하면 마커가 아이템 영역 안쪽으로 들어와 배치됨(기본값은 outside).

### 마커 종류, list-style-type
`circle`, `square`, `none`, `upper-roman`, `lower-alpha`, `decimal` 등 다양한 마커 모양을 지정할 수 있음.

### 이미지 마커, list-style-image
`list-style-image: url("marker.png")`로 사용자가 직접 만든 이미지를 마커로 사용할 수 있으며, 모든 아이템에 동일한 이미지 마커가 적용됨.

### 예제 5-9: CSS3 스타일을 응용하여 리스트로 메뉴 만들기
nav 안의 ul/li 리스트를 이용해 가로 메뉴바를 만듦. `display:inline-block`으로 아이템을 가로로 배치하고, `list-style-type:none`으로 마커를 없애고, 링크의 밑줄을 제거한 뒤 `:hover`로 마우스를 올리면 글자색이 바뀌도록 꾸밈.

---

## 5. CSS3로 표 꾸미기

### 표 테두리 제어, border
- `border`: 표 자체의 테두리
- `border-collapse: collapse`: 표와 셀의 중복된 테두리를 하나로 합침
- `table`과 `td, th`에 각각 다른 두께·색·스타일의 테두리를 지정할 수 있음

### 셀 크기 제어, width·height
`th`, `td` 선택자에 width·height를 지정해 셀 크기를 맞추며, `thead th`처럼 자손 셀렉터를 이용해 헤더 셀만 다른 높이로 지정할 수도 있음.

### 셀 여백 및 정렬
`padding`으로 셀 내부 여백을, `text-align`(left/center/right)으로 셀 내용의 정렬을 지정.

### 배경색과 테두리 효과
`border-collapse: collapse`로 이중 테두리를 제거하고, `thead`에 배경색·글자색을 지정하며, `tfoot th`나 `td`에는 아래쪽 테두리만 지정하는 등 섹션별로 다르게 꾸밀 수 있음.

### 줄무늬 만들기
`tbody tr:nth-child(even)` 가상 클래스 셀렉터로 짝수 번째 행에만 배경색(aliceblue 등)을 지정해 줄무늬 표를 만듦.

### 예제 5-10: 마우스가 올라오면 행의 배경색이 변하는 표 만들기
성적표 형태의 표에서 border-collapse로 이중 테두리를 없애고, thead/tfoot에 어두운 배경을, 짝수 행에는 옅은 배경을 입히고, `tbody tr:hover`로 마우스를 올린 행의 배경색이 pink로 바뀌도록 함.

---

## 6. 폼 꾸미기

### input 요소 색상·테두리 지정
`input[type=text]` 속성 셀렉터로 텍스트 입력창의 글자 색, 테두리(두께·스타일·둥근 모서리)를 지정할 수 있음.

### 폼 요소에 마우스 처리
- `:hover`: 마우스가 올라올 때 배경색 등을 변경 (예: `input[type=text]:hover { background: aliceblue; }`)
- `:focus`: 입력창이 포커스를 받을 때(클릭 시) 스타일 변경 (예: 글자 크기를 120%로 확대)

### 예제 5-11: 스타일로 폼 꾸미기
Name, Email, Comment, submit 버튼으로 구성된 연락처 폼에서 text/email 입력창의 글자색을 지정하고, 마우스를 올리면 배경이 aliceblue로 바뀌고, 포커스를 받으면 글자 크기가 120%로 커지도록 함. label을 block으로, 그 안의 span을 inline-block으로 지정해 라벨과 입력창을 깔끔하게 정렬.

---

## 7. CSS3 스타일로 태그에 동적 변화 만들기

CSS3만으로 자바스크립트 없이 HTML 태그 모양의 동적 변화를 줄 수 있으며, 다음 3가지 기법을 지원함.
- 애니메이션(animation)
- 전환(transition)
- 변환(transform)

### 7-1. 애니메이션(animation)
HTML 태그의 모양 변화를 시간 단위로 설정하는 기법. 작성 순서는 다음과 같음.

1. `@keyframes`로 시간별 모양 변화를 정의
```css
@keyframes textColorAnimation {
  0% { color : blue; }    /* 시작 시. 0% 대신 from 사용 가능 */
  30% { color : green; }  /* 30% 경과 시까지 */
  100% { color : red; }   /* 끝까지. 100% 대신 to 사용 가능 */
}
```
2. 애니메이션 스타일 시트 작성
```css
span {
  animation-name : textColorAnimation;   /* 애니메이션 코드 이름 */
  animation-duration : 5s;               /* 애니메이션 1회 시간 */
  animation-iteration-count : infinite;  /* 무한 반복 */
}
```

#### 예제 5-12: 애니메이션 만들기 연습
'꽝!' 글자의 크기를 3초에 걸쳐 500%에서 100%로 서서히 축소되는 애니메이션을 무한 반복으로 작성하는 연습 문제와 정답. `@keyframes`의 `from`/`to`로 시작·끝 크기를 지정하고 h3 태그에 animation 프로퍼티들을 적용.

### 7-2. 전환(transition)
HTML 태그에 적용된 CSS3 프로퍼티 값의 변화를 서서히 진행시켜 애니메이션 효과를 내는 기법. `transition: 프로퍼티 시간` 형태로 지정하며, 보통 `:hover` 등 상태 변화와 함께 사용됨.

#### 예제 5-13: font-size에 대한 전환 효과 만들기
'꽝!' 글자(span)에 `transition: font-size 5s`를 지정해, 마우스를 올리면(:hover) 글자 크기가 500%로 5초에 걸쳐 서서히 확대되는 효과를 만듦.

### 7-3. 변환(transform)
텍스트나 이미지를 회전, 확대/축소, 기울임, 이동 등 다양한 기하학적 모양으로 출력하는 기법. 회전 각도 단위는 `deg`이며 시계 방향 회전.

#### transform에 사용 가능한 2차원 변환 함수

| 구분 | 함수 | 설명 |
|---|---|---|
| 위치 이동 | `translate(x,y)` | 태그를 X축, Y축으로 x, y 만큼 이동 |
| 위치 이동 | `translateX(n)` | 태그를 X축으로 n 만큼 이동 |
| 위치 이동 | `translateY(n)` | 태그를 Y축으로 n 만큼 이동 |
| 확대/축소 | `scale(w,h)` | 태그의 폭과 높이를 각각 w, h 배 만큼 조절. w나 h를 0으로 주면 보이지 않게 됨 |
| 확대/축소 | `scaleX(n)` | 태그의 폭을 n배 만큼 조절 |
| 확대/축소 | `scaleY(n)` | 태그의 높이를 n배 만큼 조절 |
| 회전 | `rotate(angle)` | 태그를 angle 각도 만큼 시계 방향 회전 |
| 기울임 | `skew(x-angle, y-angle)` | 태그를 X축과 Y축을 기준으로 각각 x-angle, y-angle 각도만큼 기울임 변환 |
| 기울임 | `skewX(angle)` | 태그를 X축을 기준으로 angle 각도만큼 기울임 |
| 기울임 | `skewY(angle)` | 태그를 Y축을 기준으로 angle 각도만큼 기울임 |

#### 예제 5-14: 다양한 변환 사례
4개의 div에 각각 rotate(20deg), skew(0deg,-20deg), translateY(100px), scale(3,1)을 적용하고, 마우스를 올리면(:hover) 더 큰 각도·이동·배율로 추가 변환되며, scale 박스는 마우스를 누르면(:active) scale(1,5)로 또 다르게 변하는 것을 보여줌.
