# 10장. 윈도우와 브라우저 관련 객체

## 강의 목표
1. BOM, 즉 브라우저 관련 객체의 종류를 안다.
2. `window` 객체를 이해하고 윈도우 열기와 닫기 등을 제어할 수 있다.
3. `window` 객체의 타이머 기능을 활용할 수 있다.
4. `window` 객체를 이용하여 프린트, 윈도우 이동 등 다양한 제어를 할 수 있다.
5. `location` 객체로 윈도우에 로드된 문서의 주소를 알고 새 문서를 로드할 수 있다.
6. `navigator` 객체를 통해 현재 브라우저에 관한 정보를 알아낼 수 있다.
7. `screen` 객체를 통해 현재 스크린 장치의 해상도를 알아낼 수 있다.
8. `history` 객체를 이용하여 지금까지 윈도우에 로드된 웹 페이지로 이동할 수 있다.

## 1. 브라우저 관련 객체 개요

### 1.1 BOM 객체
- BOM(Browser Object Model)은 자바스크립트로 브라우저를 제어하기 위해 지원되는 객체들이다.
- HTML 페이지의 내용과는 관계없이 브라우저 자체를 제어하는 기능을 제공한다.
- 주요 BOM 객체와 기능은 다음과 같다.

| 객체 | 기능 |
|---|---|
| `window` | 브라우저 윈도우 모양 제어, 새 윈도우 열기와 닫기 |
| `navigator` | 브라우저에 대한 다양한 정보 제공 |
| `history` | 브라우저 윈도우에 로드한 URL 리스트의 히스토리 관리 |
| `location` | 브라우저 윈도우에 로드된 HTML 페이지의 URL 관리 |
| `screen` | 브라우저가 실행되고 있는 스크린 장치에 대한 정보 제공 |

- BOM은 국제 표준이 없으므로 브라우저마다 객체가 조금씩 다를 수 있다.
- 이름이 같은 BOM 객체라도 브라우저마다 프로퍼티와 메소드가 다를 수 있다.

### 1.2 BOM과 DOM
- BOM은 브라우저 관련 객체들을 의미한다.
- `window` 객체 아래에 `navigator`, `history`, `location`, `screen` 등의 객체가 있다.
- `document` 객체는 DOM(Document Object Model)에 속하며 HTML 문서의 내용과 관련된 객체이다.

## 2. window 객체

### 2.1 window 객체의 의미와 생성
- `window` 객체는 열려 있는 브라우저 윈도우나 탭 윈도우의 속성을 나타내는 객체이다.
- 브라우저 윈도우나 탭 윈도우마다 별도의 `window` 객체가 생성된다.
- 새로운 웹 페이지를 로드할 때, `<iframe>` 태그마다, 자바스크립트 코드로 윈도우를 열 때 생성된다.
- 자바스크립트 코드로 윈도우를 열 때는 `window.open()`을 사용한다.

```javascript
window.open("웹페이지 URL", "윈도우이름", "윈도우속성");
```

- `window` 객체는 `window`, `window.self`, `self`로 접근할 수 있다.

### 2.2 윈도우 모양과 프로퍼티
- `screenX`, `screenY`는 스크린에서 윈도우의 위치를 나타낸다.
- `outerWidth`, `outerHeight`는 윈도우 바깥쪽 전체 크기를 나타낸다.
- `innerWidth`, `innerHeight`는 윈도우 내부 영역의 크기를 나타낸다.

### 2.3 윈도우 열기: window.open()
- `window.open()`은 새 윈도우를 열고 웹 페이지를 출력하는 메소드이다.
- URL, 윈도우 이름, 윈도우 속성을 매개변수로 지정할 수 있다.
- 윈도우 이름에는 다음과 같은 값이 있다.
  - `_blank`: 이름 없는 새 윈도우를 열고 웹 페이지 로드
  - `_parent`: 현재 윈도우 또는 프레임의 부모 윈도우에 웹 페이지 로드
  - `_self`: 현재 윈도우에 웹 페이지 로드
  - `_top`: 브라우저 윈도우에 웹 페이지 로드
- 윈도우 이름을 지정하면 같은 이름의 윈도우가 이미 열려 있을 때 기존 윈도우에 페이지를 출력한다.

### 2.4 윈도우 닫기
- `window.close()`는 현재 윈도우를 닫는다.
- 브라우저에 따라 보안상의 이유로 현재 윈도우를 닫는 코드가 작동하지 않을 수 있다.
- 자바스크립트로 자신이 만든 윈도우는 해당 윈도우 객체의 `close()` 메소드로 닫을 수 있다.

```javascript
let win = window.open(); // 새 윈도우 생성
win.close();             // 자신이 만든 윈도우 닫기
```

### 예제 10-1: window.open()으로 윈도우 열기
- 세 개의 링크를 만들고, 링크를 클릭하면 `myWin`이라는 이름의 윈도우에 해당 사이트를 출력한다.
- 새 윈도우는 스크린의 `(300, 300)` 위치에 `400x300` 크기로 열린다.
- 세 링크가 같은 윈도우 이름을 사용하므로 하나의 윈도우를 공유한다.

### 예제 10-2: 윈도우 닫기
- 새 윈도우를 여는 기능과 윈도우를 닫는 기능을 구현한다.
- `newWin` 변수에 새로 연 윈도우 객체를 저장한다.
- 윈도우가 열리지 않았거나 이미 닫힌 경우에는 종료하고, 열려 있으면 `newWin.close()`로 닫는다.
- 현재 윈도우를 닫는 경우와 자신이 생성한 윈도우를 닫는 경우를 함께 보여준다.

## 3. window 객체의 타이머 활용

### 3.1 타이머 기능
- `window` 객체는 두 가지 타이머 기능을 제공한다.
  - 타임아웃 코드를 한 번 호출: `setTimeout()` / `clearTimeout()`
  - 타임아웃 코드를 반복 호출: `setInterval()` / `clearInterval()`

### 3.2 setTimeout() / clearTimeout()
- `setTimeout()`은 지정한 시간이 지난 후 코드를 한 번 실행한다.
- 시간은 밀리초 단위로 지정한다.
- `setTimeout()`이 반환한 타이머 ID를 이용해 `clearTimeout()`으로 실행을 취소할 수 있다.

```javascript
let timerID = setTimeout("myAlert(3)", 3000);
clearTimeout(timerID);
```

### 예제 10-3: setTimeout()로 웹 페이지 자동 연결
- 이미지 위에 마우스를 올린 상태로 5초가 지나면 네이버 웹 사이트로 이동한다.
- 5초가 지나기 전에 이미지에서 마우스를 벗어나면 `clearTimeout()`으로 타이머를 해제한다.
- `onmouseover`에서 타이머를 시작하고 `onmouseout`에서 타이머를 취소한다.

### 3.3 setInterval() / clearInterval()
- `setInterval()`은 지정한 시간 간격으로 코드를 반복 실행한다.
- 시간은 밀리초 단위로 지정한다.
- `setInterval()`이 반환한 타이머 ID를 `clearInterval()`에 전달하면 반복 실행을 중단한다.

```javascript
let timerID = setInterval("f()", 1000);
clearInterval(timerID);
```

### 예제 10-4: setInterval()로 텍스트 회전
- `setInterval()`을 이용하여 텍스트를 일정한 시간 간격으로 옆으로 회전시킨다.
- 문자열의 첫 글자를 떼어 뒤에 붙이는 방식으로 텍스트의 순서를 바꾼다.
- 텍스트를 클릭하면 `clearInterval()`을 호출하여 회전을 중단한다.

## 4. 윈도우 위치 및 크기 조절

### 4.1 윈도우 이동
- `moveBy(x, y)`는 현재 위치에서 지정한 픽셀만큼 윈도우를 이동한다.
- `moveTo(x, y)`는 스크린의 지정한 좌표로 윈도우를 이동한다.

```javascript
window.moveBy(5, 10);
window.moveTo(25, 10);
```

### 4.2 윈도우 크기 조절
- `resizeBy(x, y)`는 현재 윈도우 크기에서 가로와 세로 크기를 지정한 만큼 변경한다.
- `resizeTo(width, height)`는 윈도우 크기를 지정한 크기로 변경한다.

```javascript
window.resizeBy(-5, 10);
window.resizeTo(200, 300);
```

### 예제 10-5: 윈도우의 위치와 크기 조절
- 버튼을 클릭하여 윈도우를 왼쪽, 오른쪽, 위, 아래로 이동시킨다.
- `+`, `-` 버튼을 클릭하면 윈도우의 크기를 키우거나 줄인다.
- 강의 자료에서는 보안상의 이유로 브라우저에서 바로 실행하면 동작하지 않을 수 있으며, `window.open()`으로 생성한 윈도우 안에서는 작동한다고 설명한다.

## 5. 웹 페이지 스크롤

### 5.1 스크롤 메소드
- `scrollBy(x, y)`는 현재 스크롤 위치에서 지정한 픽셀만큼 이동한다.
- `scrollTo(x, y)`는 웹 페이지의 지정한 좌표가 윈도우의 왼쪽 위에 오도록 스크롤한다.
- 스크롤 다운은 스크롤 바를 아래로 내리는 동작이며, 웹 페이지 내용은 위로 이동한다.

```javascript
window.scrollBy(0, 10);
window.scrollTo(0, 200);
```

### 예제 10-6: 1초마다 10픽셀씩 자동 스크롤
- 웹 페이지가 로드되면 `setInterval()`로 자동 스크롤을 시작한다.
- 1초마다 `autoScroll()`을 호출하고, `window.scrollBy(0, 10)`으로 페이지를 10픽셀씩 이동시킨다.

## 6. 웹 페이지 프린트

### 6.1 window.print()
- `window.print()`를 실행하면 인쇄 다이얼로그가 열린다.
- 인쇄 다이얼로그에서 확인을 누르면 웹 페이지가 인쇄된다.

```javascript
window.print();
```

### 예제 10-7: 웹 페이지 프린트
- 링크나 버튼을 클릭하면 `window.print()`를 호출하여 현재 웹 페이지의 인쇄 다이얼로그를 연다.

### 6.2 onbeforeprint와 onafterprint
- 웹 페이지의 프린트 과정은 `onbeforeprint` 리스너 호출, 웹 페이지 프린트, `onafterprint` 리스너 호출 순서로 진행된다.
- `onbeforeprint`는 인쇄하기 전에 실행되며, 인쇄할 때만 보이게 할 내용을 표시하는 데 활용할 수 있다.
- `onafterprint`는 인쇄가 끝난 후 실행되며, 인쇄를 위해 표시했던 내용을 다시 숨길 수 있다.

### 예제 10-8: onbeforeprint와 onafterprint 이벤트 활용
- 평소에는 보이지 않는 회사 로고를 인쇄할 때만 보이도록 만든다.
- `onbeforeprint`에서 로고 영역의 `display`를 `block`으로 변경한다.
- 인쇄가 끝나면 `onafterprint`에서 `display`를 `none`으로 변경하여 로고를 다시 숨긴다.

## 7. location 객체

### 7.1 location 객체의 의미
- `location` 객체는 윈도우에 로드된 웹 페이지의 URL 정보를 나타낸다.
- `location` 객체를 이용하여 현재 윈도우에 새로운 웹 페이지를 로드할 수 있다.

```javascript
window.location = "http://www.naver.com";
window.location.href = "http://www.naver.com";
window.location.assign("http://www.naver.com");
window.location.replace("http://www.naver.com");
```

- 새 윈도우를 연 다음 그 윈도우의 `location`에 URL을 지정하여 웹 페이지를 로드할 수도 있다.

### 7.2 URL 구성 요소
- `location` 객체의 프로퍼티는 URL의 구성 요소와 연결된다.
  - `href`: URL 전체
  - `protocol`: 프로토콜
  - `hostname`: 호스트 이름
  - `host`: 호스트 이름과 포트
  - `port`: 포트
  - `pathname`: 경로
  - `search`: 검색 문자열
  - `hash`: 해시 부분

### 예제 10-9: location 객체로 웹 사이트 접속
- 선택 상자에서 웹 사이트를 선택하고 버튼을 클릭하면 선택한 사이트로 이동한다.
- 선택된 항목의 `value`를 가져와 `window.location`에 대입한다.

## 8. navigator 객체

### 8.1 navigator 객체의 의미
- `navigator` 객체는 현재 작동 중인 브라우저에 대한 다양한 정보를 나타낸다.
- 브라우저 이름, 버전, 플랫폼, 언어, 온라인 여부 등의 정보를 확인할 수 있다.

### 예제 10-10: navigator로 브라우저 정보 출력
- `navigator` 객체의 여러 프로퍼티와 메소드 값을 가져와 웹 페이지에 출력한다.
- `appCodeName`, `appName`, `appVersion`, `platform`, `product`, `userAgent`, `vendor`, `language`, `onLine`, `cookieEnabled` 등의 정보를 출력한다.
- `plugins.length`로 플러그인 개수를 확인하고, 반복문으로 각 플러그인의 이름, 설명, 파일 이름을 출력한다.

## 9. screen 객체

### 9.1 screen 객체의 의미
- `screen` 객체는 브라우저가 실행되는 스크린 장치에 관한 정보를 담고 있다.
- 화면의 크기와 사용 가능한 영역, 색상 깊이 등의 정보를 확인할 수 있다.

| 프로퍼티 | 의미 |
|---|---|
| `availHeight` | 작업 표시줄 등의 영역을 제외한 사용 가능한 화면 높이 |
| `availWidth` | 사용 가능한 화면 너비 |
| `colorDepth` | 화면의 색상 깊이 |
| `pixelDepth` | 픽셀당 색상 깊이 |
| `height` | 스크린 높이 |
| `width` | 스크린 너비 |

### 예제 10-11: 스크린 장치에 관한 정보 출력
- `screen` 객체의 `availHeight`, `availWidth`, `colorDepth`, `pixelDepth`, `height`, `width` 값을 가져와 웹 페이지에 출력한다.
- 강의 자료에서는 `height`와 `width`가 브라우저 확대/축소 설정의 영향을 받을 수 있으므로 확대/축소 값을 100%로 설정해야 정확한 값이 출력된다고 설명한다.

## 10. history 객체

### 10.1 history 객체의 의미
- `history` 객체는 윈도우에서 방문한 웹 페이지 리스트, 즉 히스토리를 나타낸다.
- `history` 객체의 메소드를 이용하여 이전 페이지나 다음 페이지로 이동할 수 있다.

| 메소드 | 기능 |
|---|---|
| `history.back()` | 이전 페이지로 이동 |
| `history.go(-1)` | 이전 페이지로 이동 |
| `history.forward()` | 다음 페이지로 이동 |
| `history.go(1)` | 다음 페이지로 이동 |

### 예제 10-12: history 객체 활용
- 버튼을 클릭하여 이전 페이지 또는 다음 페이지로 이동한다.
- `back()`과 `go(-1)`은 이전 페이지로, `forward()`는 다음 페이지로 이동하는 기능을 보여준다.
