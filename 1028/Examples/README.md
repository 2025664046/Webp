# 8장. HTML DOM과 Document

## 강의 목표
1. HTML DOM의 필요성을 이해한다.
2. DOM 트리와 HTML 페이지의 관계를 이해한다.
3. DOM 객체의 구조와 HTML 태그와의 관계를 이해한다.
4. DOM 객체를 통해 HTML 태그의 출력 모양과 콘텐츠를 제어할 수 있다.
5. document 객체를 이해하고, write() 메소드를 활용할 수 있다.
6. createElement() 등을 통해 동적으로 DOM 객체를 웹 페이지에 추가·삭제할 수 있다.

---

## 1. HTML 페이지와 자바스크립트 객체

자바스크립트 코드는 브라우저로부터 3가지 유형의 객체를 제공받아 활용함.
- **코어 객체**: Array, Date 등 자바스크립트 언어 자체가 제공하는 기본 객체
- **HTML DOM 객체**: document를 뿌리로 하는, HTML 태그가 객체화된 것들(body 등)
- **BOM 객체**: window, history 등 브라우저가 제공하는 객체

---

## 2. HTML DOM(Document Object Model)

- 웹 페이지에 작성된 HTML 태그마다 객체(DOM 객체)가 생성됨
- **목적**: HTML 태그가 출력된 모양이나 콘텐츠를 제어하기 위함
  - DOM 객체를 통해 각 태그의 CSS3 스타일 시트에 접근 및 변경
  - HTML 태그가 출력한 텍스트나 이미지 변경

### DOM 트리
- HTML 태그의 포함 관계에 따라 DOM 객체들의 트리(tree)가 생성되며, 부모-자식 관계를 가짐
- **DOM 객체**: DOM 트리의 한 노드. HTML 태그 하나당 DOM 객체 하나가 생성되며, DOM 노드(Node) 또는 DOM 엘리먼트(Element)라고도 불림

### BOM과 DOM의 관계
최상위에 `window` 객체가 있고, 그 아래에 `navigator`, `history`, `location`, `screen`, 그리고 `document`(DOM 트리의 루트)가 위치함. document 아래에는 html → head/body → title, p, span, form, input, hr 등 HTML 태그 구조 그대로 DOM 객체 트리가 생성됨.

### DOM 트리의 특징
- DOM 트리의 루트는 **document 객체**
- DOM 객체의 종류는 HTML 태그 종류만큼 존재하며, 태그 하나당 DOM 객체가 하나씩 생성됨
- HTML 태그의 포함 관계에 따라 DOM 트리에 부모-자식 관계가 형성됨

### 브라우저가 HTML 태그를 화면에 그리는 과정
1. 브라우저가 DOM 트리의 틀(document 객체) 생성
2. 브라우저가 HTML 태그를 읽고 DOM 트리에 DOM 객체 생성
3. 브라우저는 DOM 객체를 화면에 출력
4. `</html>` 태그를 만나면 document 객체를 완성하고 DOM 트리 완성
5. DOM 객체가 변경되면, 브라우저는 해당 HTML 태그의 출력 모양을 바로 갱신

→ DOM 객체를 제어하면 그에 대응하는 HTML 태그의 출력 모양에 제어 효과가 즉시 발생함.

---

## 3. HTML 태그의 요소와 DOM 객체의 구성

### HTML 태그(엘리먼트)의 5가지 구성 요소
엘리먼트 이름, 속성, CSS3 스타일, 이벤트 리스너, 콘텐츠(innerHTML)

### DOM 객체의 5가지 구성 요소

| 요소 | 설명 |
|---|---|
| 프로퍼티(property) | HTML 태그의 속성(attribute)을 반영 (예: id, tagName) |
| 메소드(method) | DOM 객체의 멤버 함수로, HTML 태그를 제어 (예: click(), focus(), setAttribute()) |
| 컬렉션(collection) | 자식 DOM 객체들의 주소를 담는 등 배열과 비슷한 집합 정보 (예: children) |
| 이벤트 리스너(event listener) | HTML 태그에 작성된 이벤트 리스너를 반영. 약 70여 개 존재 (예: onclick, onload) |
| CSS3 스타일 | 태그에 설정된 CSS3 스타일 시트 정보를 반영. style 프로퍼티로 모양 제어 가능 |

### DOM 객체 간의 관계를 나타내는 프로퍼티
- `parentElement`: 부모 DOM 객체
- `children`: 자식 DOM 객체들의 컬렉션, `childElementCount`: 자식 개수
- `firstElementChild`, `lastElementChild`: 첫째/막내 자식
- `previousElementSibling`, `nextElementSibling`: 형제(sibling) 관계의 이전/다음 DOM 객체 (없으면 null)

### 예제 8-1: DOM 객체의 구조 출력 — p 객체 사례
`document.getElementById("firstP")`로 p 태그의 DOM 객체를 찾아, id, tagName, innerHTML, style.color, onclick, childElementCount, offsetWidth, offsetHeight 등 다양한 프로퍼티 값을 alert()로 출력.

---

## 4. DOM 객체 다루기

### DOM 객체 찾기, document.getElementById()
```js
let p = document.getElementById("firstP"); // id 값이 firstP인 DOM 객체 리턴
p.style.color = "red";                     // p 객체의 글자 색을 red로 변경
```

### DOM 객체의 CSS3 스타일 동적 변경
하이픈(`-`)이 포함된 CSS3 프로퍼티 이름은 카멜 표기법으로 바뀜: `background-color` → `backgroundColor`, `font-size` → `fontSize`.
```js
let span = document.getElementById("mySpan");
span.style.color = "green";
span.style.fontSize = "30px";
span.style.border = "3px dotted magenta";
```

### 예제 8-2: `<span>`의 CSS3 스타일 동적 변경
버튼 클릭 시 change() 함수가 호출되어, mySpan의 글자색·크기·display(block)·폭·테두리·여백을 한꺼번에 바꾸어 인라인 박스가 블록 박스로 변경되는 모습을 보여줌.

### innerHTML 프로퍼티
- 시작 태그와 종료 태그 사이에 들어 있는 HTML 콘텐츠를 나타내는 프로퍼티
- innerHTML 값을 수정하면 해당 HTML 태그의 콘텐츠가 즉시 변경됨
```js
let p = document.getElementById("firstP");
p.innerHTML = "나의 <img src='puppy.jpg'>강아지입니다.";
```

### 예제 8-3: innerHTML을 이용하여 HTML 콘텐츠 동적 변경
p 태그를 클릭하면 change() 함수가 호출되어 innerHTML을 "나의 `<img>` 강아지" 텍스트로 바꿔, 글자 대신 강아지 이미지가 나타나도록 함.

### this 키워드
- 객체 자신을 가리키는 자바스크립트 키워드로, DOM 객체 안에서 자기 자신을 가리키는 용도로 사용됨
```html
<div onclick="this.style.backgroundColor='orange'">
<button onclick="this.style.backgroundColor='orange'">
```

### 예제 8-4: this 활용
버튼이나 div를 클릭하면 `onclick="change(this, ...)"`처럼 this(클릭된 자기 자신의 DOM 객체)를 change() 함수에 전달해, 클릭된 요소마다 각기 다른 글자색·크기로 바뀌도록 함.

---

## 5. document 객체

- HTML 문서 전체를 대변하는 객체이며, DOM 객체를 접근하는 경로의 시작점이자 DOM 트리의 최상위 객체
- 프로퍼티는 HTML 문서의 전반적인 속성을, 메소드는 DOM 객체 검색·생성·문서 전반 제어 기능을 제공
- 브라우저는 HTML 문서를 로드하기 전에 document 객체를 먼저 생성한 뒤, 이를 뿌리로 DOM 트리를 만듦
- `window.document` 또는 `document`로 접근
- **주의**: document 객체 자체는 DOM 객체가 아니며 연결된 스타일 시트가 없음 → `document.style.color = "red";`는 오류

### 예제 8-5: document 객체의 프로퍼티 출력
문서가 완전히 로드된 뒤(onload) `location`, `URL`, `title`, `head.id`, `body.style.color`, `domain`, `lastModified`, `defaultView`, `readyState`, `referrer`, `activeElement.value`, `documentElement.tagName` 등 document의 주요 프로퍼티를 alert로 출력하고, input 태그에 포커스를 줌.

---

## 6. DOM 트리에서 DOM 객체 찾기

### 태그 이름으로 찾기, document.getElementsByTagName()
태그 이름이 같은 모든 DOM 객체를 찾아 컬렉션으로 리턴.
```js
let divTags = document.getElementsByTagName("div");
let n = divTags.length; // <div> 태그의 개수
```

### 예제 8-6: 태그 이름으로 DOM 객체 찾기, getElementsByTagName()
버튼을 클릭하면 모든 `<span>` 태그를 getElementsByTagName()으로 찾아, 각 span의 글자색을 orchid, 크기를 20px로 한꺼번에 변경.

### class 속성으로 찾기, document.getElementsByClassName()
class 속성이 같은 모든 DOM 객체를 찾아 컬렉션으로 리턴.
```js
let plainClasses = document.getElementsByClassName("plain");
let n = plainClasses.length;
```

### 예제 8-7: class 속성으로 DOM 객체 찾기, getElementsByClassName()
"가고 싶은 곳"/"먹고 싶은 것" 버튼을 각각 클릭하면, class="place" 또는 class="food"인 모든 span 태그를 getElementsByClassName()으로 찾아 색·크기·밑줄 등 스타일을 일괄 변경.

---

## 7. document.write()와 document.writeln()

### HTML 페이지 로딩 과정
1. 브라우저는 HTML 페이지 로드 전 빈 상태의 document 생성
2. 브라우저는 HTML 페이지를 위에서 아래로 해석
3. HTML 태그들을 document 객체에 담아감(DOM 객체 생성)
4. `</html>` 태그를 만나면 document 객체를 완성하고 닫음

### write()
document 객체에 담긴 HTML 콘텐츠의 마지막에 HTML 태그를 추가. 추가된 태그는 DOM 객체로 바뀌어 DOM 트리에 삽입되고 화면에 즉시 출력됨.
```js
document.write("<h3>Welcome to my home</h3>");
document.write(2+3); // 5 출력
```

### writeln()
HTML 텍스트 뒤에 `'\n'`을 덧붙여 출력하지만, HTML에서는 줄바꿈 대신 빈칸 하나 정도의 효과만 남음. 줄을 바꾸려면 `document.write("<br>");`를 사용해야 함.

### 예제 8-8: write()와 writeln() 메소드 활용
write()를 여러 번 호출해 h3, p 태그, 숫자 연산 결과(2+3)를 출력하고, writeln()은 다음 줄로 넘어가지 못하고 빈 칸만 생기는 차이를 비교.

### write()를 잘못 사용하는 예
문서 로드가 끝난 뒤(이벤트 등에 의해) write()를 호출하면, 기존에 출력되어 있던 HTML 콘텐츠 전체가 지워지고 새 내용으로 덮어써짐.

### 예제 8-9: write()를 잘못 사용하는 예
body의 onclick에 `document.write('<h3>클릭되었습니다</h3>')`를 지정해, 바탕을 클릭하면 기존 페이지 내용이 모두 지워지고 새 h3 문구만 남는 것을 보여줌.

---

## 8. document의 열기와 닫기, open()과 close()

- **document.open()**: 현재 브라우저에 출력된 HTML 콘텐츠를 지우고 새로운 HTML 페이지를 시작(즉 DOM 트리를 지우고 새로 시작)
- **document.close()**: 현재 브라우저에 출력된 HTML 페이지를 완성함. 이후로는 document.write()를 호출할 수 없음

```js
document.open();
document.write("<html><head>...<body>안녕하세요.");
document.write("......");
document.write("</body></html>");
document.close();

// 새 윈도우를 열고 그곳에 HTML 문서 출력
let newWin = window.open("", "outWin", "");
newWin.document.open();
newWin.document.write("<html><head>...<body>안녕하세요.");
newWin.document.write("......");
newWin.document.write("</body></html>");
newWin.document.close();
```

### 예제 8-10: HTML 문서 작성 연습 페이지 만들기
textarea에 사용자가 HTML 코드를 입력하고 버튼을 클릭하면, `window.open()`으로 새 창을 열고 그 창의 document에 open() → write(textArea.value) → close()를 호출해 입력한 HTML을 새 창에 렌더링함.

---

## 9. 문서의 동적 구성

### DOM 객체 동적 생성, document.createElement("태그이름")
지정한 태그 이름의 DOM 객체를 새로 생성.
```js
let newDIV = document.createElement("div");
newDIV.innerHTML = "새로 생성된 DIV입니다.";
newDIV.setAttribute("id", "myDiv");
newDIV.style.backgroundColor = "yellow";
```

### DOM 트리에 삽입
- `부모.appendChild(DOM객체);`: 부모의 마지막 자식으로 추가
- `부모.insertBefore(DOM객체 [, 기준자식]);`: 기준 자식 앞에 삽입
```js
let p = document.getElementById("p");
p.appendChild(newDiv); // 생성한 div를 p 태그의 마지막 자식으로 추가
```

### DOM 객체의 삭제
```js
let myDiv = document.getElementById("myDiv");
let parent = myDiv.parentElement;
parent.removeChild(myDiv); // 부모에서 myDiv 객체 삭제
```

### 예제 8-11: HTML 태그의 동적 추가 및 삭제
링크를 클릭하면 createDIV() 함수가 실행되어 새 `<div>` 태그(DOM 객체)를 createElement()로 만들고 내용·id·배경색을 지정한 뒤 appendChild()로 body에 삽입하며, 삽입된 div를 클릭하면 removeChild()로 자기 자신을 부모로부터 제거해 다시 사라지도록 함.
