# 항해 18일차

## 오늘 할 일

새로운 팀과 인사 하기
한 주 일정 보고 강의량 정해서 듣기 => 2주차 강의 완료하고 과제 제출하기

## 리액트2 1주차 1강(1주차 오늘 배울 것)

- 1주차
  자바스크립트 문법  
   프로젝트 틀 만들기

- 2주차
  로그인 이론(OAuth2.0)  
   파이어베이스 인증을 통한 로그인 기능

- 3주차
  이미지 업로드 관련 자바스크립트 문법  
   파이어베이스 활용 이미지 프리뷰

- 4주차
  무한 스크롤 관련 자바스크립트 문법(debounce, throttle)
  무한스크롤, 알림기능

- 5주차
  검색엔진 최적화 이론  
   검색엔진 최적화

## 리액트2 1주차 2강(필수 프로그램 설치 안내)

pass

## 리액트2 1주차 3강(Javascript Re-Start(1) 기본)

변수: 재할당이 가능한 것(var, let)
var는 변수를 같은 이름으로 여러개 선언 가능, 함수레벨 스코프(함수 내 에서 자유롭게 사용 가능)👎  
 let은 블록레벨 스코프(if, for 구문 등 의 블록 내에서만 사용 가능, 범위가 더 좁다고 할 수 있겠다.)👍
상수: 재할당이 불가능한 것(const)
블록레벨 스코프

```javascript
// 1. var
var a = 1;
console.log(a);

var a = 2; // 재선언 O
console.log(a); // 2

a = 3; // 재할당 O
console.log(a); // 3

////////////////////////

// 2. let
let a = 1;
console.log(a);

let a = 2; // 재선언 X
console.log(a); // Error

a = 3; // 재할당 O
console.log(a); // 3

/////////////////////////

// 3. const
const a = 1;
console.log(a);

const a = 2; // 재선언 X
console.log(a); // Error

a = 3; // 재할당 X
console.log(a); // Error
```

```javascript
//var 과 호이스팅(선언 맨 위로 올리기)
// 자바스크립트는 파일을 읽고, 파일을 실행한다.
//변수등을 파일을 읽으면서 실행할 환경을 정하고(실행 컨텍스트), 파일을 실행한다.
//실행 컨텍스트 진행 시 let, const와 다르게 var를 제일 위로 올려주기 때문에(호이스팅) 제일 밑에서 var를 선언해도 위에서 사용이 가능하다.

function cat() {
  name = "perl";

  console.log(name);

  var name;
}
cat(); //perl O

function cat() {
  name = "perl";

  console.log(name);

  let name; // const도 에러
}
cat(); //Error

//let과 const가 호이스팅이 안되는 이유는 변수를 실행 컨텍스트에 등록할 때 선언(어떤걸 쓸지 보여줌), 초기화(메모리 공간 확보), 할당(확보한 메모리 공간에 값을 넣어 주는 것)의 세 단계를 거쳐서 하는데, let, const는 실행컨텍스트에서 선언만 하고, 올려주는데 파일이 차례대로 실행될 때 변수가 선언 된 곳이 읽히는 순간 초기화가 이루어지기 때문이다. var는 선언과 초기화를 동시에 하기 때문에 호이스팅이 가능하다.

//정리하자면 let, const 선언, 호이스팅은 이루어지나, 초기화가 되지 않아서 그렇다. 이러한 오류현상을 TDZ(Temporary Dead Zone)이라고 한다.
```

자료형:  
원시자료형[숫자, bigInt, 문자, boolean, undefined(값이 할당되지 않음), null(값이 존재하지 않음), 심볼형(고유 식별자)],

객체자료형[객체형]

```javascript
let cat = Symbol("cat");

let cat2 = Symbol("cat");

console.log(cat == cat2); // false
//같은 값이어도 고유의 값으로 만든다!
```

## 리액트2 1주차 4강(Javascript Re-Start(2) 객체)

이전 시간에 자료형을 왜 원시형과 객체형으로 나눴을까? => 객체는 여러 자료형을 담을 수 있는 구조이기 때문!

객체형 자료는 다음과 같은 구성을 가지고 있다.

```javascript
{
  key: value;
} // 이러한 한 쌍을 프로퍼티라고 한다.
// 주의! key값을 무조건 문자형으로 들어간다! 숫자를 넣어도 문자형으로 인식

let a = { b: 1, c: 2 };
a.b; // 1
a["c"]; // 2

//배열도 객체형이 맞다!
const array = [0, 1, 2]; //키 값이 없지만 숫자로 접근 가능
//array[0]

///////////////////

//객체 선언
//객체 생성자로 만들기
let cat = new Object();

//객체 리터럴로 만들기
//중괄호로 객체를 선언하는 걸 리터럴이라고 하는데, 객체 선언할 때 주로 쓴다!
let cat = {};

//자바스크립트 엔진은 리터럴 선언을 하면 new Object로 변환해서 넣어준다
```

![객체는 왜 수정할 수 있을까?](/images/react2_week1/1.PNG)

객체는 왜 const로 주어져도 수정할 수 있을까?  
=> 정답은 const에 저장되는 것은 객체가 아닌 객체가 저장되어 있는 곳을 알려주는 주소이기 때문이다. 그래서 const의 다른 자료형들처럼 선언, 초기화 할당을 똑같이 거친다. 객체는 따로 객체만 저장되는 공간이 있다.(객체의 property는 보호되지 않는다.)

## 리액트2 1주차 5강(Javascript Re-Start(3) 함수)

함수는 행동을 가능하게하는 특별한 객체다 라고 생각하면 좋다.

함수 표현법

```javascript
// 함수 선언문
function cat() {
  console.log("cat");
}
//선언문 사용 시 선언과 초기화가 동시에 되므로(var 처럼) 선언한 위치보다 위에서 사용이 가능하다.

// 함수 표현식
let cat = function () {
  console.log("perl");
};
//실행 컨텍스트가 실행될 때 cat을 선언 하고 구문 실행시 함수를 초기화(함수가 만들어지고) 하고 실행 한다. this(함수 자체)

//화살표 함수
let cat2 = () => {
  console.log("perl2");
};
//함수표현식의 단축 표현 그러나 this(위에 있는 부모), 생성자로 사용불가, 제너레이터로 사용불가

//생성자 비추👎
let dog = new Function("alert('wow')");

//함수는 만들어질 때 렉시컬 환경을 참조한다.
//[[Envionment]]라는 숨겨진 프로퍼티에 위치 저장

function b() {
  let p = 1;
  let a = new Function("alert(p)");
}
b();

// 이렇게 함수를 만들어버리면 아니되오...
// 생성자로 함수를 만들면 항상 바깥에 있는 것으로 인식이 되어 사용하기가 불편하다(전역변수 이슈)
```

지역변수, 외부변수, 스코프

```javascript
function b() {
  let p = 1; //function a 입장에서 외부변수
  let a = function () {
    let p = 2;
    console.log(p);
  };

  a();
}
b();

//지역변수는 함수 내에서만 사용 가능
//p는 재할당 한게 아니라 외부변수 내부변수로 다른 함수다. 내부 함수에서는 내부변수가 우선시 되기 때문에 콘솔 창에 2가 뜨는 것이다.
```

콜백함수

```javascript
fucntion useBall(cat) {
    console.log(cat, "공으로 노는 중!");
}

function playWithCat(cat, action) {
    action(cat);
}
playWithCat("perl", useBall);
//perl 공으로 노는 중!

//인수로 전달되는 useBall 같은 함수를 콜백함수라고 한다.

//매개변수, 인수?
//객체는 주소가 메모리에 저장되어 변경되어도 괜찮은데 콜백 함수는 그 값이 바뀌면 어떡하지?
//그래서 인수가 되는 함수(useBall)를 복사한 것을 사용한다. 이 복사된 인수(argument)를 매개변수(parameter)라고 한다.
```

## 리액트2 1주차 6강(Prototype)

프로토타입이란?: 디자인 패턴 중 하나로써, 객체 생성시 사용되는 리소스를 최대한 절감하려는 방식  
원본 객체가 있을 때 그것을 복사해서 새 것으로 이용하는 방식  
객체는 함수를 통해서 만들어진다. 자바스크립트는 프로토타입 기반 언어이다.  
자바스크립트에서 객체를 생성하면 함수의 프로토타입(원본) 객체를 복사해서 생성한다.(⭐)  
객체는 어디에서 복사되어 생성되었는지 기록이 되어있다.(⭐)

![프로토타입](/images/react2_week1/2.PNG)

Animal 함수를 만들었는데 Animal.prototype도 만들어 진 것이고, 이 안에는 constructor와 proto 라는 값이 들어간다.  
여기서 proto는 prototype link를 의미하며, 부모링크의 내용을 나타내는 것이다. 그렇다면 최초 원본(프로토타입) 까지 체인이 형성되고, 그것을 프로토타입 체인이라고 한다.

## 리액트2 1주차 7강(프로젝트 세팅(1) - 프로젝트 생성)

크롬 확장프로그램
React-developer-tool  
 컴포넌트 구조를 볼 수 있게 해준다.
Redux-Devtool  
 리덕스 흐름을 볼 수 있게 해준다.

## 리액트2 1주차 8강(프로젝트 세팅(2) - 기획서 쪼개기)

화면 구성을 어떻게 짤지 나누는 방법  
뷰로 쪼개기  
데이터로 쪼개기  
큰 화면에서 작게 쪼개가면서 만드는 방법 사용  
![컴포넌트](/images/react2_week1/3.PNG)
헤더, 인풋, 버튼은 재사용이 가능하다!

![컴포넌트2](/images/react2_week1/4.PNG)  
헤더, 포스트(사진, 작성자, 좋아요)은 재사용 가능!

![컴포넌트3](/images/react2_week1/5.PNG)  
위의 포스트는 또 image, text, button을 재사용하여 활용 가능!

데이터는 어떻게 나눌것인지도 고민해봐야 한다.  
사용자가 여러명일 때 포스트 처리 등...  
기획서 컴포넌트로 쪼개는 연습 필요  
항상 적당한 크기와 사용법을 가진 컴포넌트가 제일 좋다!

## 리액트2 1주차 9강(메인페이지(포스트목록)만들기)

어떻게 컴포넌트를 나누고, 폴더를 나누는지가 중요!

- src
  - components: 중간단위 컴포넌트 폴더
  - elements: 최소단위 컴포넌트 폴더
  - pages: 한 페이지 컴포넌트 폴더
  - shared: 공용으로 사용하는 폴더(App.js 파이어베이스 파일)

## 리액트2 1주차 10강(최소단위 컴포넌트 만들기(1))

<></> === <React.Fragment></React.Fragment>

페이지 라우팅

![컴포넌트3](/images/react2_week1/6.PNG)

자세하게 만들기전에 위치 잡아주기

포스트의 기본 props 설정  
Post 의 props를 받는 Grid 생성 => props로 받을 스타일링 작업 완료(삼항연산자) => Post에서 Grid 컴포넌트를 불러 값을 주면 props로 내려받아 Grid에서 스타일링에 사용

## 리액트2 1주차 11강(최소단위 컴포넌트 만들기(2))

## 리액트2 1주차 12강(최소단위 컴포넌트 만들기(3))

index.js에서 import 통합

## 일기

상담결과:  
아이디어 보단 기술적인 요소를 어필해라!
그러면 복잡하게 생각하지 말고 아이디어보다 시각화 기술, 인터랙션을 예리하게 갈고 닦는다는 생각으로 접근하는 것이 맞을 것 같다.

이것이 미다님이 말하신 아토믹 디자인 패턴인가😨  
1주차 강의는 진짜 정신없게 지나갔다. 강의는 완료했지만 아직도 구조가 정확하게 이해가지 않는다. 중요한 점은 큰 페이지 => 중간 컴포넌트 => 제일 작은 컴포넌트의 구조로 이루어진다는 것이다. 연습 또 연습해서 몸에 익히도록 하자!
