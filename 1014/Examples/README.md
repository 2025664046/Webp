# 7장. 자바스크립트 코어 객체와 배열

## 강의 목표
1. 객체의 기본 개념을 간단히 이해한다.
2. 브라우저가 제공하는 기본 객체(코어 객체)들의 종류를 알고 사용할 수 있다.
3. Date 객체를 활용할 수 있다.
4. String 객체를 활용할 수 있다.
5. 자바스크립트 배열을 만들 수 있다.
6. Array 객체를 이용하여 배열을 만들고 활용할 수 있다.
7. Math 객체를 활용할 수 있다.

---

## 1. 객체 개념

- 현실 세계는 객체들의 집합(사람, 책상, 자동차, TV 등)이며, 각 객체는 자신만의 고유한 구성 속성을 가짐
  - 자동차: `<색상:오렌지, 배기량:3000CC, 제조사:한성, 번호:서울1-1>`
  - 사람: `<이름:이재문, 나이:20, 성별:남, 주소:서울>`
  - 은행계좌: `<소유자:황기태, 계좌번호:111, 잔액:35000원>`

### 자바스크립트 객체의 구성
- 여러 개의 **프로퍼티(property)**와 **메소드(method)**로 구성됨
- 프로퍼티: 객체의 고유한 속성(변수) / 메소드: 함수

```js
let account = {
  owner : "황기태",
  code : "111",
  balance : 35000,
  deposit : function() { … },
  withdraw : function() { … },
  inquiry : function() { … }
};
```

---

## 2. 자바스크립트 객체 종류

자바스크립트는 **객체 기반 언어**이며(객체 지향 언어는 아님), 객체의 유형은 다음 3가지로 나뉨.

1. **코어 객체**: 자바스크립트 언어가 실행되는 어디서나 사용 가능한 기본(표준) 객체. Array, Date, String, Math 타입 등. 웹 페이지와 서버 모두에서 사용 가능
2. **HTML DOM 객체**: HTML 문서의 각 태그들을 객체화한 것으로, 문서의 내용과 모양을 제어하기 위한 W3C 표준 객체
3. **브라우저 객체**: 브라우저를 제어하기 위한 BOM(Browser Object Model) 객체로, 비표준 객체

---

## 3. 코어 객체

- 종류: Array, Date, String, Math 등
- 생성: `new` 키워드 이용 (객체 생성 시 내부에 프로퍼티와 메소드가 자동으로 존재)
- 접근: 객체와 멤버 사이에 점(`.`) 연산자 사용

```js
let today = new Date();            // Date 타입 객체 생성
let msg = new String("Hello");     // String 타입 객체 생성

obj.프로퍼티 = 값;        // 프로퍼티 값 변경
변수 = obj.프로퍼티;      // 프로퍼티 값 읽기
obj.메소드(매개변수 값들); // 메소드 호출
```

### 예제 7-1: 자바스크립트 객체 생성 및 활용
Date 객체를 생성해 `toLocaleString()`으로 현재 시간을 출력하고, String 객체를 생성해 문자열 내용과 `length` 프로퍼티(읽기 전용)를 출력.

---

## 4. 자바스크립트 배열

- 여러 개의 원소들을 연속적으로 저장해 전체를 하나의 단위로 다루는 데이터 구조
- 0에서 시작하는 인덱스로 각 원소에 접근

```js
let cities = ["Seoul", "New York", "Paris"];
let name = cities[0];        // name은 "Seoul"
cities[1] = "Gainesville";   // "New York" 자리에 "Gainesville" 저장
```

### 배열 만드는 2가지 방법
1. **`[]`로 배열 만들기**: 대괄호 안에 초기값을 나열. 배열 크기는 고정되지 않고 원소 추가 시 자동으로 늘어남
   - 주의: 현재 배열보다 큰 인덱스에 원소를 추가하면 중간에 비어있는(`undefined`) 원소들이 생김
2. **Array 객체로 배열 만들기**: 초기값을 가진 배열, 일정 크기만 지정한 배열, 빈 배열 등 다양한 방식으로 생성 가능

```js
let week = ["월","화","수","목","금","토","일"];
let plots = [-20, -5, 0, 15, 20];
plots[5] = 33;   // 6번째 원소 추가, 크기 6이 됨
plots[10] = 33;  // 크기가 11이 되고 plots[7]~plots[9]는 undefined

let week = new Array("월","화","수","목","금","토","일"); // 초기값으로 생성
let week = new Array(7);  // 7개 원소 크기만 지정
let week = new Array();   // 빈 배열 생성
```

### 예제 7-2: `[]`로 배열 만들기
정수 5개를 담은 배열을 만들고, for문과 while문으로 각 원소 값만큼 `*`를 반복 출력한 뒤 원소 값도 함께 출력.

### 예제 7-3: Array 객체로 배열 만들기
빈 배열(`new Array()`)을 만든 뒤 인덱스로 온도 값 6개를 하나씩 채워 넣고, `length` 프로퍼티만큼 반복해 평균 온도를 계산.

### 배열의 원소 개수, length 프로퍼티
- 배열의 크기는 Array 객체의 `length` 프로퍼티로 확인하며, 사용자가 임의로 값을 바꿔 배열 크기를 늘리거나 줄일 수 있음

```js
let plots = [-20, -5, 0, 15, 20];
let m = plots.length;   // m은 5
plots.length = 10;      // 크기가 5에서 10으로 늘어남
plots.length = 2;       // 크기가 2로 줄어 나머지 원소는 삭제됨
```

### 예제 7-4: Array 객체의 메소드 활용
`concat()`, `join()`, `reverse()`, `slice()`, `sort()`, `toString()` 메소드를 차례로 호출해, 원본 배열이 변경되는 메소드와 새 배열/문자열을 반환하는 메소드의 차이를 비교.

### 배열의 특징
배열은 그 자체로 Array 객체이며(`[]`로 생성해도 동일), 한 배열 안에 숫자·문자열·객체·함수 등 서로 다른 타입의 데이터를 섞어 저장할 수 있음.

---

## 5. Date 객체

시간 정보를 담는 객체로, 현재 시간이나 특정 날짜를 생성해 다룰 수 있음.

```js
let now = new Date();                  // 현재 날짜와 시간으로 초기화
let startDay = new Date(2017, 2, 1);   // 2017년 3월 1일(2는 3월을 의미)
let date = now.getDate();   // 오늘 날짜
let hour = now.getHours();  // 현재 시
```

### 예제 7-5: Date 객체 생성 및 활용
현재 시간을 가진 Date 객체를 생성해 `toUTCString()`으로 출력하고, `getFullYear()`, `getMonth()`, `getDate()`, `getHours()`, `getMinutes()`, `getSeconds()`, `getMilliseconds()`로 각 요소를 분리 출력하며, 특정 날짜(`new Date(2023,7,15,12,12,12)`)로 만든 객체도 `toLocaleString()`으로 출력.

### 예제 7-6: 방문 시간에 따라 변하는 배경색 만들기
현재 시간의 초(`getSeconds()`)가 짝수면 violet, 홀수면 lightskyblue로 `document.body.style.backgroundColor`를 바꿔 페이지 배경색이 방문 시점에 따라 달라지게 함.

---

## 6. String 객체

- 문자열을 담기 위한 객체이며, 한 번 생성된 String 객체의 내용은 수정되지 않음(메소드 호출 시 새 문자열/객체가 생성됨)
- `length` 프로퍼티(읽기 전용)로 문자열 길이 확인, `[]` 연산자로 배열처럼 각 문자 접근 가능

```js
let hello = new String("Hello");
let res = hello.concat("Javascript"); // concat() 후에도 hello는 변화 없음

let m = hello.length;   // m은 5
let c = hello[0];       // c = "H"
```

### 예제 7-7: String 객체의 메소드 활용
`charAt()`, `concat()`, `indexOf()`, `slice()`, `substr()`, `toUpperCase()`, `replace()`, `trim()`, `split()` 메소드를 차례로 호출해 결과를 출력하고, 메소드 실행 후에도 원본 문자열 a, b는 변하지 않음을 확인.

---

## 7. Math 객체

- 수학 계산을 위한 프로퍼티와 메소드를 제공하며, `new Math()`로 객체를 생성하지 않고 바로 사용
- `Math.random()`: 0 이상 1 미만의 난수(실수) 리턴
- `Math.floor(m)`: m의 소수점 이하를 제거한 정수 리턴

```js
let sq = Math.sqrt(4);       // 4의 제곱근, 2
let area = Math.PI*2*2;      // 반지름 2인 원의 면적

for(let i=0; i<10; i++) {
  let m = Math.random()*100;  // 0~99.999...의 실수 난수
  let n = Math.floor(m);      // 0~99 사이의 정수
}
```

### 예제 7-8: Math를 이용한 구구단 연습
`Math.random()`과 `Math.floor()`로 1~9 사이의 난수 두 개를 만들어 구구단 문제를 생성하고, `prompt()`로 입력받은 답을 `eval()`로 계산한 정답과 비교해 정답/오답을 판정.

---

## 8. 사용자 객체 만들기

사용자가 새로운 타입의 객체를 만드는 3가지 방법:
1. `new Object()`로 직접 객체 만들기
2. 리터럴 표기법(`{ }`)으로 직접 객체 만들기
3. 객체의 틀인 **프로토타입(생성자 함수)**을 만들어 `new`로 객체 생성하기

### 8-1. new Object()로 객체 만들기
1. `new Object()`로 빈 객체 생성
2. 프로퍼티 이름과 초기값을 지정해 프로퍼티 추가
3. 메소드로 쓸 함수를 미리 작성한 뒤 메소드 이름에 함수를 지정해 추가

```js
let account = new Object();
account.owner = "황기태";
account.code = "111";
account.balance = 35000;
account.inquiry = inquiry;
account.deposit = deposit;
account.withdraw = withdraw;
```

### 예제 7-9: new Object()로 계좌를 표현하는 account 객체 만들기
`inquiry()`, `deposit()`, `withdraw()` 함수를 미리 작성해 두고, `new Object()`로 만든 빈 객체에 계좌 관련 프로퍼티와 이 함수들을 메소드로 추가해 입출금 및 잔액 조회를 수행.

### 8-2. 리터럴 표기법으로 만들기
중괄호(`{ }`)를 이용해 객체의 프로퍼티와 메소드를 한 번에 지정하는, 가장 많이 사용되는 방법.

```js
let account = {
  owner : "황기태",
  code : "111",
  balance : 35000,
  inquiry : function () { return this.balance; },
  deposit : function(money) { this.balance += money; },
  withdraw : function (money) {
    this.balance -= money;
    return money;
  }
};
```

### 예제 7-10: 리터럴 표기법으로 계좌를 표현하는 account 객체 만들기
예제 7-9와 동일한 account 객체를 리터럴 표기법으로 한 번에 작성해 동일하게 입출금 및 잔액 조회 동작을 확인.

### 8-3. 프로토타입(prototype)
- 객체의 모양을 가진 틀(예: 붕어빵 틀). C++, Java의 클래스에 해당
- Array, Date, String도 자바스크립트가 제공하는 프로토타입이며, `new 프로토타입()`으로 객체 생성
- 사용자 정의 프로토타입은 함수(생성자 함수)로 만들며, `this.프로퍼티명 = 값` 형태로 프로퍼티와 메소드를 정의한 뒤 `new` 연산자로 객체를 생성

```js
function Student(name, score) {
  this.univ = "한국대학";
  this.name = name;
  this.score = score;
  this.getGrade = function () {
    if(this.score > 80) return "A";
    else if(this.score > 60) return "B";
    else return "F";
  }
}
let kitae = new Student("황기태", 75);
let jaemoon = new Student("이재문", 93);
```

### 예제 7-11: 프로토타입으로 객체 만들기
Account 생성자 함수(프로토타입)를 작성해 owner, code, balance 프로퍼티와 inquiry/deposit/withdraw 메소드를 정의하고, `new Account(...)`로 객체를 생성해 입출금 및 잔액 조회 동작을 확인.
