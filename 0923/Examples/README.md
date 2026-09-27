# 4장. CSS3로 웹 페이지 꾸미기

## 강의 목표
1. CSS3 언어가 무엇인지 안다.
2. CSS3 스타일 시트를 작성하는 방법을 안다.
3. CSS3 셀렉터 만드는 방법을 안다.
4. CSS3로 텍스트 꾸미기를 할 수 있다.
5. CSS3로 웹 페이지에 색과 모양을 꾸밀 수 있다.
6. CSS3의 박스 모델을 이해하고 다룰 수 있다.
7. CSS3로 HTML 태그의 배경과 테두리 등을 꾸밀 수 있다.
8. CSS3로 그림자 효과를 만들 수 있다.

---

## 1. CSS3 스타일 시트

- **CSS(Cascading Style Sheet)**: HTML 문서의 색이나 모양 등 외관을 꾸미는 언어
- CSS로 작성된 코드를 **스타일 시트(style sheet)** 라고 부름
- 현재 표준은 **CSS3**이며, CSS1 → CSS2 → CSS3 → CSS4(표준화 진행 중) 순으로 발전
- CSS3의 주요 기능: 색상과 배경, 텍스트, 폰트, 박스 모델, 비주얼 포맷 및 효과, 리스트, 테이블, 사용자 인터페이스

### 예제 4-1: HTML 태그로만 작성한 웹 페이지
CSS 없이 순수 HTML만 사용했을 때 브라우저 기본 스타일로 출력되는 모습을 보여줌.

### 예제 4-2: CSS3 스타일 시트로 꾸민 웹 페이지
body, h3, hr, span 태그에 배경색·글자색·테두리·글자크기를 지정해 꾸밈.

---

## 2. CSS3 스타일 시트 구성

```
span { color : blue; font-size : 20px; } /* span 태그 스타일 선언 */
```

- **셀렉터**: CSS3 스타일 시트를 HTML 페이지에 적용하도록 만든 이름
- **프로퍼티**: 스타일 속성 이름(약 200개 정도 존재)
- **값**: 프로퍼티의 값
- **주석문**: `/* ... */` 형태로 여러 줄, 아무 위치에나 작성 가능
- **대소문자 구분 없음**: `body`와 `BODY`는 동일하게 취급

---

## 3. HTML 문서에 CSS3 스타일 시트 작성하는 방법 (3가지)

1. `<style></style>` 태그에 스타일 시트 작성
2. HTML 태그의 `style` 속성에 스타일 시트 작성
3. 스타일 시트를 별도 파일로 작성 후 `<link>` 태그나 `@import`로 불러 사용

### 3-1. `<style>` 태그에 스타일 시트 만들기
- `<style>` 태그는 `<head>` 태그 내에서만 사용
- 여러 번 작성 가능하며, 작성된 스타일들이 합쳐져 사용됨
- 웹 페이지 전체에 적용됨

#### 예제 4-3: `<style>` 태그로 스타일 시트 만들기
head 안에 style 태그를 넣어 body 배경색, 좌우 여백, h3 정렬·색상을 지정.

### 3-2. style 속성에 스타일 시트 만들기
- HTML 태그의 style 속성에 CSS3 스타일 시트를 직접 작성
- 해당 태그에만 스타일이 적용됨

#### 예제 4-4: style 속성에 스타일 시트 만들기
모든 p 태그에 공통 스타일을 적용하면서, 일부 p 태그에는 style 속성으로 개별 스타일을 덮어씀.

### 3-3. 외부 스타일 시트 파일 불러오기
- `.css` 파일에 스타일 시트를 저장해 여러 페이지에서 재사용
- 동일 스타일 중복 작성을 없애고 사이트 전체 디자인 일관성 확보
- 불러오는 방법: `<link>` 태그 이용, `@import` 이용

#### 예제 4-5: `<link>` 태그로 CSS3 파일 불러오기
외부 mystyle.css 파일을 link 태그로 연결해서 스타일 적용.

#### 예제 4-6: @import로 CSS3 파일 불러오기
style 태그 안에서 @import 구문으로 외부 mystyle.css를 불러와 적용.

---

## 4. CSS3 규칙

### 4-1. 스타일 상속
- CSS3 스타일은 부모 태그로부터 자식 태그로 상속됨
- 예: `<p>` 태그는 `<em>`의 부모 태그이며, `<em>`은 부모 `<p>`의 색상 스타일을 상속받음

#### 예제 4-7: 부모 스타일 상속
부모 태그(p)에 지정한 스타일을 자식 태그(em)가 상속받는 것을 확인.

### 4-2. 스타일 합치기(cascading)와 오버라이딩(overriding)
태그에 적용 가능한 스타일 우선순위(낮음 → 높음):
1. 브라우저의 디폴트 스타일
2. 스타일 시트 파일(external.css)에 선언된 스타일
3. `<style></style>` 태그에 선언된 스타일
4. style 속성에 선언된 스타일

→ 모든 스타일이 합쳐지고, 동일한 프로퍼티는 순위가 높은 쪽이 우선 적용됨.

#### 예제 4-8: 여러 스타일 시트가 중첩되는 경우
외부 CSS 파일, style 태그, style 속성이 동시에 적용될 때 우선순위에 따라 최종 스타일이 정해지는 과정을 보여줌.

---

## 5. 셀렉터(Selector)

HTML 태그의 모양을 꾸밀 스타일 시트를 선택하는 기능. 여러 유형이 있음.

| 셀렉터 유형 | 설명 |
|---|---|
| 태그 이름 셀렉터 | 태그 이름 자체가 셀렉터로 사용. 같은 이름의 모든 태그에 적용 |
| class 셀렉터 | 점(`.`)으로 시작. HTML의 class 속성으로 지정. class 속성이 같은 모든 태그에 적용 |
| id 셀렉터 | `#`으로 시작. HTML의 id 속성으로 지정. id는 원래 태그를 유일하게 구분하는 목적이라 중복 없이 사용하는 것이 바람직 |
| 자식 셀렉터 | `부모 > 자식` 형태로 부모의 직계 자식에만 적용 (예: `div > strong`) |
| 자손 셀렉터 | `조상 자손` 형태로 자식뿐 아니라 그 하위 모든 후손에 적용 (예: `ul strong`) |
| 전체 셀렉터 | `*` 와일드카드로 모든 태그에 적용 |
| 속성 셀렉터 | 특정 속성 값이 일치하는 태그에만 적용 (예: `input[type=text]`) |
| 가상 클래스 셀렉터 | 특정 조건/상황에서 스타일 적용. `:hover`, `:active`, `:focus`, `:link`, `:visited`, `:first-letter`, `:first-line`, `:nth-child()` 등 40개 이상 존재 |

- id 셀렉터는 특정 태그 하나에만 스타일을 적용할 때 적합
- class 셀렉터는 여러 태그를 묶어 그룹 단위로 동일한 스타일을 적용할 때 적합

#### 예제 4-9: 셀렉터 활용
태그 이름 셀렉터, 자식/자손 셀렉터, class 셀렉터, id 셀렉터, 가상 클래스 셀렉터(:first-letter, :hover)를 한 페이지에서 종합적으로 사용.

---

## 6. CSS3에서 색 표현

3가지 표현 방법:
1. **16진수 코드**: `#8A2BE2`
2. **10진수 코드(RGB 함수)**: `rgb(138, 43, 226)`
3. **색 이름**: `blueviolet` (CSS3 표준에서 140개 색 이름 정의)

### 색 관련 프로퍼티
```
color : 색             /* 텍스트 글자색 */
background-color : 색  /* 배경 색 */
border-color : 색      /* 테두리 색 */
```

#### 예제 4-10: 색 활용
색 이름, 16진수 코드로 여러 div의 배경색을 지정하고 margin으로 간격을 줌.

---

## 7. 텍스트 꾸미기

```
text-indent : <length>|<percentage>;  /* 들여쓰기 */
text-align : left|right|center|justify;  /* 정렬 */
text-decoration : none|underline|overline|line-through;  /* 밑줄/취소선/윗줄 등 */
```

#### 예제 4-11: 텍스트 꾸미기
text-align(정렬), text-decoration(밑줄/취소선/윗줄), text-indent(들여쓰기)로 문단과 링크를 꾸밈.

---

## 8. 폰트

- 폰트 형: Serif(세리프 있음), Sans-Serif(세리프 없음), Monospace(글자 폭 동일)

### 폰트 제어 프로퍼티
```
font-family : Arial, "Times New Roman", Serif;  /* 폰트 패밀리, 콤마로 우선순위 나열 */
font-size : 40px | medium | 1.6em;              /* 폰트 크기 */
font-style : italic;                             /* 이탤릭 */
font-weight : 300 | bold;                        /* 굵기(100~900) */
```

### 단축 프로퍼티, font
```
font : font-style font-weight font-size font-family;
/* 예: font : italic bold 20px consolas, sans-serif; */
```

#### 예제 4-12: CSS3 폰트 활용
font-family, font-size, font-weight, font-style, font 단축 프로퍼티로 다양한 폰트 효과를 적용.

---

## 9. CSS3의 박스 모델(Box Model)

HTML 태그는 사각형 박스로 다루어지며, 각 요소를 하나의 박스(콘텐츠-패딩-테두리-여백)로 취급.

### 박스 모델의 구성
- **콘텐츠**: 텍스트나 이미지가 출력되는 부분
- **패딩(padding)**: 콘텐츠를 직접 둘러싸는 내부 여백
- **테두리(border)**: 패딩 외부의 테두리
- **여백(margin)**: 박스의 맨 바깥 영역, 테두리 바깥에서 이웃 태그와의 거리

### 박스 모델 구성 프로퍼티

| 구분 | 콘텐츠 | 패딩 | 테두리 | 여백 |
|---|---|---|---|---|
| 크기 | width, height | padding-top/right/bottom/left | border-top/right/bottom/left-width | margin-top/right/bottom/left |
| 크기 단축 | - | padding | border-width | margin |
| 스타일 | - | - | border-top/right/bottom/left-style | - |
| 스타일 단축 | - | - | border-style | - |
| 색 | - | (패딩 자체 색 없음, 배경색으로 표현) | border-top/right/bottom/left-color | 투명(부모 배경 비침) |
| 색 단축 | - | - | border-color | - |
| 전체 단축 | - | - | border | - |

#### 예제 4-13: `<div>`의 박스 모델 보이기
margin, border, padding에 각각 다른 색을 입혀서 박스 모델의 구조(콘텐츠-패딩-테두리-여백)를 시각적으로 확인.

#### 예제 4-14: 박스 모델 활용
이미지가 든 div에 padding, border(점선), margin을 적용해 실제 박스 모델을 꾸밈.

---

## 10. 테두리(Border)

### 10-1. 테두리 선 스타일
`solid, none, hidden, dotted, dashed, double, groove, ridge, inset, outset` 등 다양한 스타일 지원.

#### 예제 4-15: 다양한 테두리 선 스타일
solid, none, hidden, dotted, dashed, double, groove, ridge, inset, outset 등 border-style 종류를 비교.

### 10-2. 둥근 모서리 테두리 - border-radius
```
border-radius : 50px;                      /* 4개 모서리 모두 동일 */
border-radius : 0px 20px 40px 60px;        /* 좌상→우상→우하→좌하 시계방향 순서 지정 */
```

#### 예제 4-16: 다양한 둥근 모서리 테두리
border-radius 값을 다르게 주어 모서리가 둥근 정도와 대칭 구조가 달라지는 것을 비교.

### 10-3. 이미지 테두리 만들기 - border-image
테두리를 모서리(corner)와 에지(edge)로 구분해 이미지를 입힘. border-width, border-style을 먼저 지정해야 함.
```
border-image : url("border.png") 30 round;
/* round: 반복 배치(길이에 맞춤), repeat: 반복 배치, stretch: 늘여서 배치 */
```

#### 예제 4-17: 이미지 테두리 만들기
border-image로 테두리에 이미지를 입히고, round/repeat/stretch 방식에 따른 배치 차이를 비교.

---

## 11. 배경(Background)

```
background-color : skyblue;                         /* 배경색 */
background-image : url("spongebob.png");            /* 배경 이미지 */
background-position : center center;                /* 배경 이미지 위치 */
background-repeat : repeat-y | no-repeat | repeat-x; /* 반복 방식 */
background-size : 100px 100px;                       /* 배경 이미지 크기 */
```
- background-color와 background-image가 함께 지정되면, 이미지가 없는 영역에 배경색이 출력됨

### 단축 프로퍼티, background
```
background : skyblue url("spongebob.png") center center/100px 100px repeat-y;
```

#### 예제 4-18: `<div>` 박스에 배경 꾸미기
background-color, background-image, background-size, background-repeat, background-position을 조합해 배경 이미지를 반복 배치.

---

## 12. 그림자 효과

### 12-1. 텍스트 그림자, text-shadow
```
text-shadow : h-shadow v-shadow blur-radius color | none;
```
- h-shadow, v-shadow: 원본과 그림자의 수평/수직 거리(필수)
- blur-radius: 흐림 정도(선택)
- color: 그림자 색
- none: 그림자 없음

#### 예제 4-19: text-shadow로 텍스트 그림자 만들기
기본 그림자, 색상 그림자, 흐림 효과, 네온(glow), 워드아트, 3D, 다중 그림자 효과를 비교.

### 12-2. 박스 그림자, box-shadow
```
box-shadow : h-shadow v-shadow blur-radius spread-radius color | none | inset;
```
- spread-radius: 그림자 크기(선택, 기본 0)
- inset: 박스 안쪽에 그림자를 넣어 음각처럼 보이게 함

#### 예제 4-20: box-shadow로 박스 그림자 만들기
div 박스 전체에 단색 그림자, 흐린 그림자, 다중 그림자 효과를 적용.

---

## 13. 마우스 커서 제어, cursor

```
cursor : value;
/* value: auto, crosshair, default, pointer, move, copy, help, progress,
   text, wait, none, zoom-in, zoom-out, e-resize, ne-resize, nw-resize,
   n-resize, se-resize, sw-resize, s-resize, w-resize, uri 중 하나 */
```

#### 예제 4-21: 마우스 커서
cursor 프로퍼티로 십자, 도움말, 포인터, 진행 중, 크기 조절 등 다양한 마우스 커서 모양을 태그별로 지정.
