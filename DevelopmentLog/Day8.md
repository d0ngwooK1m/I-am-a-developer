# 항해 8일차

## 리액트 1주차 1강(OT)
첫주차엔 생각보다 리액트에 대해서 많이 공부하지 않는다. 대신 리액트에 필요한 사전지식을 많이 공부할 것이다.  
  
어떻게 배울 것인가
* 오류를 많이 내본다. 빨간화면에 익숙해지기
* 모르는 단어를 많이 들어볼 것이다. 키워드 찾으면서 공부하기
* 만든 코드를 주저없이 버리고 새로 시작하기  

질문할 때는(진짜 모르겠을 때는)  
* 어떤 운영체제를 쓰는지
* 오류가 났다면 어떤 오류 메세지가 나오는지(화면 캡쳐)
* 어떤 것을 하고 싶은지  

알려주면 좋다.  

## 리액트 1주차 2강(설치)
설치할 항목들  
* NVM  

나는 WSL을 사용해서 zsh 기준으로 파일을 받고 환경변수 설정을 해줬다. 설정 후 NVM nodejs npm 모두 버전 확인을 하였다.

## 리액트 1주차 3강(웹 기초지식)
웹을 구성하는 요소: 서버(주인)와 클라이언트(손님)  

웹이란?: 서버와 클라이언트의 상호작용!
![flow_of_web_service](/images/react_week1/1.png)
집주인이 손님에게 필요한 데이터와 정적자원(html, css, javascript)을 주는 것이다.  
서버  <-(요청)- 클라이언트  
서버  -(응답)-> 클라이언트  

우리가 하는 일은?: 화면을 그리고, 데이터를 끼얹는다!

서버리스(파이어베이스)란?: 서버가 없다는 뜻이 아니라 백엔드 작업을 할 필요없이 설정된 서버를 사서 쓴다는 뜻. 즉 서버리스=/=백엔드리스  
우리는 프론트엔드 작업에 더 신경을 쓸 수 있다.

## 리액트 1주차 4강(HTML 기초지식)  
HTML: 마크업
오늘의투두 HTML로 짜보기 => 성공!😎
여러가지 태그(div, p)들을 부르는 명칭: 요소  
DOM: HTML요소 하나 하나를 객체로 생각하는 모델
![tree_of_DOM](/images/react_week1/2.png)  
document = 현재 DOM을 모두 포함해 보여줌  
document.body = 도큐먼트 자식 노드인 바디를 보여줌
같은 레벨에 있는 요소: 형제관계(head, body)
DOM요소 접근  
* document.body.childNodes => children보다 더 상세하게 나타내는 방법인듯?
* document.body.children => body안에 있는 자식요소들을 전부 표현한다.
* document.getElementsByTagName('div') => 특정한 태그만 가져오고 싶을 때 사용  

모든 접근방법은 https://developer.mozilla.org/ko/docs/Web/API/Document 참조  

## 리액트 1주차 5강(CSS 기초지식)  
전체적인 참조는 https://developer.mozilla.org/ko/docs/Web/CSS  
Selector: 어떤걸 꾸밀지 선택하는 것  
* 여러 요소 선택: #id, .class {...} 으로 여러 요소를 선택 가능하다. 모든 요소를 자유롭게 선택할 수 있다.
* 수도 클래스 선택: 어떤 요소가 특정상태(hover 등) 일 때 button:hover {...} 으로 표현할 수 있다.

CSS 예시와 똑같이 꾸미기 성공!😎  
작업은 중간중간 자주 확인할 것  
그리드 시스템: 레이아웃을 어떻게 잡을 것인가?
* 박스모델: 마진(보더 바깥 간격주기)-보더-패딩(내용과 보더 사이의 간격주기)-내용 순으로 구성. 모든 요소는 박스모델로 이루어져 있다.
* 그리드 시스템: alt+shift+F 이쁘게 정리 flex 맛보기, 그리드 시스템 =/= display:grid
* CSS 사칙연산: 연산을 통해 여러 기기를 사용하는 사용자들에게 이쁘게 보이기 위해 작성
    * invalid property value: calc() 내부 계산식에서 연산자 앞 뒤를 붙여쓰면 발생하는 오류, 값이 적용이 안된다. https://zetawiki.com/wiki/CSS_calc_invalid_property_value

## 리액트 1주차 6강(JS 기초지식1)
자바스크립트로 DOM 접근하기
1. document.getElementsByClassName
```javascript
const wraps = document.getElementsByClassName('wrap');
console.log(wraps);
```
결과값으로 나오는 HTMLCollection은 배열과 비슷한 유사 배열이며, 배열 접근방식을 사용할 수 있다.(length나 [번호] 접근법) 그러나 map, filter와 같은 배열 내장함수를 사용할 수는 없다.

2. document.getElementById
```javascript
const title = document.getElementById("title");
console.log(title);
```

3. document.getElementsByTagName
```javascript
const buttons = document.getElementsByTagName("button");
console.log(buttons);
```

4. document.createElement("태그명")
```javascript
const new_div = document.createElement("div");
new_div.style.backgroundColor = "green";
new_div.style.width = "100px";
new_div.style.height = "100px";
console.log(new_div);
document.body.appendChild(new_div);
//스타일 지정후 body에 붙이기
```

## 리액트 1주차 7강(JS 기초지식2)
1. let, const와 Scope  
    let으로 선언하고 할당한 변수는 재할당 가능, const는 재할당 불가능  
    var이 둘과 다른점은 var는 함수레벨 스코프를 가지고, let, const는 블록레벨 스코프를 가진다.
```javascript
function scope() {
    const a = 0;
    let b = 0;
    var c = 0;

    //{}블록 => 블록레벨스코프: 블록 안에서만 살아있다.
    if(a === 0) {
        const a = 1;
        let b = 1;
        var c = 1;
        
        console.log(a, b, c);
        // 1 1 1
        //이 블록 안에서 const, let은 다른 a,b이다. 그러나 c는 항상 같다.
    }
    console.log(a, b, c);
    // 0 0 1
    //c는 함수레벨 변수이기 때문에 scope함수 전체에서 살아있다. 그래서 변경된 값이 유지된다.
}
```
2. 함수  
    미리 코드 묶음을 만들어 놓고 실행하는 것
```javascript
//1. 함수 선언식
function do_something (변수) {...};

//2. 함수 표현식
let do_something = function [함수명](변수) {...}

//3. 화살표 함수, 함수 표현식의 단축형
let do_something = (변수) => {...}
```

3. 클래스
    클래스가 어떻게 생겼는지에 대해 알면 좋다. => 리액트 컴포넌트(클래스형, 함수형) 배울 때 좋다.  

```javascript
class Cat {
    //생성자 함수
    constructor(name) {
        //여기서 this는 이 클래스(Cat)를 지칭
        //Cat.name을 하면 여기에 있는 name이 나온다.
        this.name = name;
    }
    showName() {
        console.log(this.name);
    }
}

let cat = new Cat("perl");
//new는 새로운 클래스를 만드는데 사용
cat.showName();
//perl
cat
//Cat {name: "perl"}

let cat2 = new Cat("two");
cat2
//Cat {name: "two"}

//상속
class MyCat extends Cat {
    constuctor(name, age) {
        //super는 상속 받을 클래스에서 가져올 수 있는 기능
        super(name);
        this.age = age;
    }
    showName() {
        console.log(this.name + "입니다.");
    }
    showAge() {
        console.log(this.age);
    }
}

let my_cat = new MyCat("perl", 4);
my_cat.showAge();
my_cat.showName();
//perl입니다. 상속받아 똑같은 함수 사용하면 마지막에 만든 함수가 실행됨.
```

4. = 과 == 과 ===  

![javascript_meme](/images/react_week1/3.png)  
엌ㅋㅋ 이러는 이유는 자바스크립트는 "묵시적 형변환" 프로그래밍 언어이기 때문이다.(아마 To-Scribble 프로젝트에서 파일명 랜덤값 문제는 이 때문인듯)  
```javascript
1 + "2"
"12"
```
* =  
    할당
* ==  
    유형을 따지지 않고 비교  
    (1 == "1" -> true)
* ===  
    유형을 따지고 비교  
    (1 === "1" -> false)

5. 스프레드 문법
```javascript
let a1 = [1, 2, 3];
let a2 = [3, 4, 5];
let a3 = [...a1, ...a2];
a3
//[1, 2, 3, 3, 4, 5]
//안에 있는 요소를 끄집어 내서 사용할 때 사용
//redux 불변성에서 자세히 다룸
```

6. 삼항연산자
보통은 return 문에 if문을 못쓰지만 삼항연산자를 사용하면 축약 형태로 표현할 수 있다.  
```javascript
let info = {name : "mean0", id: 0};

let is_me = info.name === "mean0"? true : false;
//조건 ? 참 : 거짓
console.log(is_me);
```  

## 리액트 1주차 8강(JS 기초지식3)
Array의 내장함수 4개!
1. map  
요소에 대한 가공가능(가공 조건 줌)
```javascript
const array_num = [0, 1, 2, 3, 4, 5];
//배열에 속해있는 요소들을 전부 변환해주고 싶을 때 사용, 반복문을 쓴다고 생각하자
const new_array = array_num.map((array_item) => {
    return array_item + 1;
});
new_array;
//[1, 2, 3, 4, 5, 6]
array_num;
//[0, 1, 2, 3, 4, 5] 원본배열을 건드리지 않는다!
```

2. filter  
요소에 대한 가공불가(넣을 수 있는 조건만 줌)
```javascript
//어떠한 조건에 부합하는 요소만 넣는다
const array_num = [0, 1, 2, 3, 4, 5];
const new_array = array_num.filter((array_item) => {
    return array_item > 3;
});
new_array;
// [4, 5];
array_num;
// [0, 1, 2, 3, 4, 5];
```

3. concat  
```javascript
const array_num = [0, 1, 2, 3, 4, 5];
const new_array = array_num.filter((array_item) => {
    return array_item > 3;
});
const merge = array_num.concat(new_array);
merge
// [0, 1, 2, 3, 4, 5, 4, 5];
//concat은 중복제거를 하지 않는다.

//스프레드 문법과 new Set으로 중복 제거된 배열 만들기
const merge2 = [...new Set([...array_num, ...new_array])];
merge2;
// [0, 1, 2, 3, 4, 5,];
```

4. from  
```javascript
const my_name = "dongwoo";
const my_name_array = Array.from(my_name);
my_name_array;
// [d, o, n, g, w, o, o]
//나는 split()으로 나눴었는데 이게 활용도가 높다고 하니 이제부터 이걸 쓰도록 노력하자!
const num_array = Array.from(my_name, (item, index) => {
    return index;
});
// [0, 1, 2, 3, 4, 5, 6]

const new_array = Array.from({length: 4}, (item, index) => {
    return index;
});
new_array
// [0, 1, 2, 3]
//from은 이미 있는 값도 넣을 수 있고, length같은 속성도 넣어줄 수 있다.
```

5. reduce()  
https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce  

퀴즈1 map으로 고양이 세기
![map_quiz](/images/react_week1/4.PNG)  

return count++; 도 결과엔 문제 없는 것 같다. 왜냐하면 위에 for문이랑 같다고 생각하면 함수가 종료되어도 다음 for 순서로 넘어가기 때문이다.  
  
퀴즈2 filter로 고양이 넣어주기
![filter_quiz](/images/react_week1/5.PNG)  

indexOf로 체크하는 부분 다시한번 보자! 고양이가 포함되지 않으면 -1을 리턴하는 구조이다.

퀴즈3 concat으로 동물농장 만들기
![filter_quiz](/images/react_week1/6.PNG)  

첨엔 실수로 스프레드 방식으로 풀었다. 근데 잘된다ㅋㅋㅋ  
이렇게도 풀 수 있구나 오히려 좋아

## 리액트 1주차 9강(첫 React 프로젝트 만들기)
리액트는 노드 위에서 동작한다.  
노드는 업데이트 양이 많고 빠르다.  
매번 노드를 직접 관리하기는 너무 힘들다.
NVM은 각 프로젝트에 어떤 버전의 노드를 쓸지 관리하게 해준다!  
npm은 노드 패키지를 관리해주는 매니저이다.  
npm으로 yarn(또 다른 노드 패키지 매니저) 설치하기  
> npm install -g yarn  

여기서 -g는 global의 약자이다. 전역적(어디서나 쓸 수 있게)으로 설치하라는 뜻  
yarn이 좀 더 빠르기 때문에 앞으로 패키지 설치는 yarn으로 할 예정  
  
CRA(Create React App)는 편하게 리액트 프로젝트를 시작할 수 있게 해주는 패키지
> yarn add global create-react-app  

> yarn create react-app week-1  
설치하는데 10분정도 걸렸음...ㅋㅋㅋ  
리액트 작업에 필요한 파일들이 담긴 week-1폴더가 생성됨.  
작업은 week-1 폴더 안의 src 폴더에서 작업.

> cd week-1  
yarn start  

localhost:3000 으로 리액트 기본파일이 실행된다. 시간이 좀 걸리니 기다릴 것  

## 리액트 1주차 10강(JSX)
src 폴더의 app.js 파일을 뜯어보자!  
```javascript
import logo from './logo.svg';
import React from "react";
import './App.css';

function App() {
  return (
    <div className="App">
      <header className="App-header">
        <img src={logo} className="App-logo" alt="logo" />
        <p>
          Edit <code>src/App.js</code> and save to reload.
        </p>
        <a
          className="App-link"
          href="https://reactjs.org"
          target="_blank"
          rel="noopener noreferrer"
        >
          Learn React
        </a>
      </header>
    </div>
  );
}

export default App;
//리액트에서는 html파일을 다룰 수 있다.
//리액트에서는 jsx 문법을 사용하여 리액트 요소를 만들어주고, 이 요소를 DOM 위에 렌더링 시켜 뷰를 그려준다.
```
왜 저장해도 새로고침이 안될까....  
문제 해결:  
> I had the same issue with WSL2.
.env with the content of CHOKIDAR_USEPOLLING=true helped.  
https://github.com/facebook/create-react-app/issues/9904


## 리액트 1주차 11강(JSX 사용법)
1. 태그는 꼭 닫아주기  
2. 무조건 1개의 엘리먼트를 반환하기  
3. JSX에서 javascript 값을 가져오려면?  
4. class 대신 className!  

## 리액트 1주차 12강(Quiz_간단한 텍스트 입력 화면 만들기)  

## 리액트 1주차 13강(끝&숙제설명)  

## 일기  
겁나 힘들다... 양이 너무 많다. 내일 2주차 할 수 있을까...?