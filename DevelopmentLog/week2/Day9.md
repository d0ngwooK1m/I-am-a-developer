# 항해 9일차

## 리액트 2주차 1강(라이프 사이클이란?)  

라이프 사이클을 이해하기 위해 필요한 지식  
* 가상돔:  
> 실제 돔에서는 컴포넌트가 변경될때마다 바뀌는게 부담 되니까 가짜 돔을 만들고, 가짜돔에 변경사항을 올리고 진짜 돔과 비교하여 마지막에 변경사항만 진짜 돔에서 바꾸는 방식을 사용한다.  

그러나 사이트 구조에 따라 진짜 돔이 더 빠를 수 있기 때문에 잘 골라서 사용하자!  

* 라이프 사이클:  
> 컴포넌트(웹을 이루는 구성요소)가 나타났다가 사라지기까지의 과정  

![life_cycle](/images/react_week2/1.PNG)  
크게 생성-수정-삭제 세단계로 나뉜다.  

## 리액트 2주차 2강(라이프 사이클 함수로 보는 라이프 사이클)  
  
주의☹) 현재 리액트는 공식적으로 클래스형 컴포넌트보다 함수형 컴포넌트 사용을 적극 권장하고 있는 상태이다.  

그런데 라이프 사이클은 클래스형 컴포넌트이다.  
왜 라이프 사이클을 배워야 할까? => 함수형 컴포넌트에서 라이프 사이클 역할을 하는 react hooks는 주기를 한 눈에 파악하기 힘들기 때문!  
그만큼 라이프 사이클의 개념이 중요하기 때문인듯 하다.  
그리고 공부하는 중 둘 다 써볼 예정이다.  

코드예제  
생성이 될 때 작동하는 함수  
```javascript
constructor(props) {
    super.props

    this.state = {
        cat_name: "나비"
    }
}
```
바뀔 때 작동하는 함수  
```javascript
ender() {

console.log('in render!');

return (
<div>
{/* render 안에서 컴포넌트의 데이터 state를 참조할 수 있습니다. */}
<h1>제 고양이 이름은 {this.state.cat_name}입니다.</h1>
<button onClick={this.changeCatName}>고양이 이름 바꾸기</button>
</div>
);
//이후 componenetDidUpdate 작동
```

작업이 완료되고 돔에 완전히 올라갈 때 작동하는 함수
```javascript
componentDidMount() {
    console.log("in componentDidMount!");
}
//페이지 생성될 때에만 작동, 새로고침 하면 작동X
//이미 가상돔이 실제돔으로 올라간 뒤 이기 때문에 DOM 조작이나 AJAX addEventListener 넣는데 사용 가능
```

이름이 변경됐을 때 작동하는 함수  
```javascript
componentDidUpdate(prevProps, prevState) {
    console.log(prevProps, prevState);
    console.log("in componentDidUpdate!");
}
//콘솔 창
//{}(이전에 부모가 준 요소) {cat_name: "나비"}(이전에 있던 상태)
//in componentDidUpdate!
//이미 가상돔이 실제돔으로 올라간 뒤 이기 때문에 DOM 조작이나 AJAX addEventListener 넣는데 사용 가능
```
이름이 삭제됐을 때 작동하는 함수  
```javascript
componentWillUnmount() {
    console.log("in componentWillUnmount");
}
//화면에서 완전히 사라지기 직전에 호출
```

## 리액트 2주차 3강(Component1: State와 Props)  
컴포넌트 구조

![life_cycle](/images/react_week2/2.PNG)  
스파르타 코딩 사이트의 컴포넌트 구조는 다음과 같이 위에서 부터 헤더, 이미지, 콘텐츠, 푸터로 이루어져 있을 것이다.  
HTML 태그 구성요소를 간단하게 나타내면 다음과 같다.  
```javascript
1. <header/>
2. <container/>
    1. <imagebanner/>
    2. <contents1/>
3. <footer/>
```  

State:  
    State는 컴포넌트가 가지고 있는 데이터
    ex) header컴포넌트는 온라인, 오프라인, 기업교육 등의 state를 가지고 있고, header 안에서 state를 삭제하거나 추가할 수 있다.  

Props:
    Props는 Component가 부모 Component로부터 받아온 데이터이다.  
    예를 들어, 위 이미지의 이미지 배너와 컨텐츠1 태그는 컨테이너로 부터 필요한 정보들을 props로 내려받아 사용하고 있다.  

Props는 변경할 수 없고, State는 변경할 수 있다.  

## 리액트 2주차 4강(Component2: 함수형 Component)  

코딩룰(코드 컨벤션): 폴더이름은 소문자로, js나 컴포넌트파일은 첫글자가 대문자인 카멜케이스로 작성!

```javascript
//BucketList.js
import React from "react";
//리액트 패키지에서 리액트를 가져와

const BucketList = (props) => {

    return (
        <div>버킷 리스트</div>
    );
};

export {BucketList};
export default BucketList;
//외부에서 이 파일을 쓸 수 있게 해준다.
//둘 다 결과는 같음
```  

```javascript
//App.js
import './App.css';

import {BucketList} from "./BucketList.js";
// import BucketList from './BucketList';
//import 하는 방법 2가지 역시 결과는 같음
// ./는 현재폴더 ../는 상위폴더 ../../는 상위의 상위 폴더

function App() {
  return (
    <div className="App">
      <BucketList/>
    </div>
  );
  //  BucketList 적용할 때 태그로 적용
}

export default App;

```  

## 리액트 2주차 5강(Component3: 클래스형 Component)  
버킷리스트의 뼈대를 만들어보며 클래스형 컴포넌트를 알아보자!

```javascript
//BucketList.js
import React from "react";
//리액트 패키지에서 리액트를 가져와

const BucketList = (props) => {
    console.log(props);
    return (
        <div>버킷 리스트</div>
    );
};
//어디서 정보를 주는 것일까? 그렇기 때문에 인자가 props일것이다.

export default BucketList;
//외부에서 사용할 수 있게 export
```  

```javascript
import React from "react";
import BucketList from './BucketList';

class App extends React.Component {
  constructor(props) {
    super(props);

    this.state = {
      list: ["옷이랑 신발사기", "하루동안 아무것도 안하기", "자전거 타기"],
    }
  }

  render() {
    console.log(this.state.list)
    return (
      <div className="App">
        <BucketList list_test={this.state.list}/>
      </div>
    );
  }
}
//React.Component라는 부모 클래스를 받아서 App이라는 클래스를 만듦
//여기서도 state가 아니고 props로 받네? React.Component가 본체인 것일까?
//아무튼 상위 클래스에서 props를 super로 상속받음 그리고 this.state라는 변수를 만듦
//그리고 렌더로 결과값 쓰기
//왜 new 키워드를 안써도 되는거지? 원래 그런건감

export default App;
```

## 리액트 2주차 6강(Quiz_버킷리스트 만들기, 중요!)

```javascript
//BucketList.js
// 리액트 패키지를 불러옵니다.
import React from 'react'; 

// 함수형 컴포넌트는 이렇게 쓸 수도 있고
// function Bucketlist(props){
// return (
// <div>버킷 리스트</div>
// );
// }

// 이렇게 쓸 수도 있어요. =>가 들어간 함수를 화살표 함수라고 불러요.
// 저희는 앞으로 화살표 함수를 사용할거예요.
// 앗 () 안에 props! 부모 컴포넌트에게 받아온 데이터입니다.
// js 함수가 값을 받아오는 것과 똑같이 받아오네요.
const BucketList = (props) => {

// Quiz 1: my_list에 ['a', 'b', 'c'] 대신 부모 컴포넌트가 넘겨준 값을 넣으려면 어떻게 해야할까요?

const my_lists = props.list;
console.log(props);

// 컴포넌트가 뿌려줄 ui 요소(리엑트 엘리먼트라고 불러요.)를 반환해줍니다.
return (
<div>
{
// js의 내장 함수 중 하나인 map입니다. 리스트의 갯수만큼 => 오른쪽 구문을 반복해요. 
// 자세한 사용법은 아래 링크를 확인해주세요.
// https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/map
my_lists.map((list, index) => {
// 콘솔을 확인해봅시다 :)
console.log(list);
return (<div key={index}>{list}</div>);
})
}
</div>
);
}

// 우리가 만든 함수형 컴포넌트를 export 해줍니다.
// export 해주면 다른 컴포넌트에서 BucketList 컴포넌트를 불러다 쓸 수 있어요.
export default BucketList;
```  
BucketList.js에서 App.js의 App에서 인자를 받아오기 때문에 props로 오는 것이었다. { list }를 인자로 받아오면 props.list처럼 접근할 필요없이 list로 접근할 수 있다.

```javascript
import React from "react";
import "./App.css";
import BucketList from './BucketList';

class App extends React.Component {
  constructor(props) {
    super(props);

    this.state = {
      list: ["옷이랑 신발사기", "하루동안 아무것도 안하기", "자전거 타기"],
    }
  }

  render() {
    console.log(this.state.list)
    return (
      <div className="App">
        <h1>내 버킷리스트</h1>
        <BucketList list={this.state.list}/>
      </div>
    );
  }
}

export default App;
```  
App.js에서 BucketList를 import한 다음 h1태그 밑에 위치시킨다. 그 다음 App 클래스에서 만든 this.state.list를 BucketList태그에 list라는 이름의 변수로 담아서 주는 것이다.  
즉, BucketList.js의 props는 this.state(props)이거나 this.state.list({list}) 인것이다.  

## 리액트 2주차 7강(CSS in React)  
기존의 style = {{ background: "green" }} 이 방식의 스타일링을 inline 스타일링이라고 한다.  

![마진여백상쇄](/images/react_week2/3.PNG)  
h1에 마진이 있는데 .App이 밀려난 것처럼 보인다. 이를 마진여백상쇄 현상이라고 한다.  
해결: h1 display 속성을 inline-flex(마진이 없게) 주면 된다.  

CSS순서는 실제 HTML 순서와 최대한 같도록!!  

## 리액트 2주차 8강(-styled-component)  
터미널 분할을 하는이유? 리액트를 계속 실행하면서 패키지도 받고 싶기 때문에  
꼭 진행하는 프로젝트 폴더 안에서 받고 받은 뒤 package.json 안의 dependency에 받아져 있는지 확인할 것
> yarn add styled-components  

styled-components를 쓰면 좋은 점 
1. 간단한 화살표 함수 사용가능 () => {...} 말고 () => (결과) 
2. 삼항연산자도 사용가능 () => (a ? b : c) 
3. scss도 사용가능  
```javascript
import React from "react";
import BucketList from './BucketList';
import "./style.css";
import styled from "styled-components";

class App extends React.Component {
  constructor(props) {
    super(props);

    this.state = {
      list: ["옷이랑 신발사기", "하루동안 아무것도 안하기", "자전거 타기"],
    }
  }

  render() {
    console.log(this.state.list)
    return (
      <div className="App">
        <MyStyled>
          <p>I'm Here!!</p>
        </MyStyled>
        {/* <div className="container">
          <h1>내 버킷리스트</h1>
          <hr className="line" />
          <BucketList list={this.state.list}/>
        </div> */}
      </div>
    );
  }
}

const MyStyled = styled.div`
  width: 50vw;
  height: 150px;
  background-color: ${(props) => (props.bg_Color ? "red": "purple")};
  p {
    color: white;
  }
  &:hover {
      background-color: blue;
  }
`;
//여기서 적용가능, 항상 마지막에 ; 붙이는거 잊지말 것! 없으면 실행 안 됨
//네스팅은 하위 태그에 포함되는 요소의 스타일을 현재 스타일 안에 쓸 수 있는 방법
//&는 styled component scss 분법에서 나 자신을 가리키는 표시!

export default App;
```

## 리액트 2주차 9강(Quiz_버킷리스트에 styled-components 적용하기)
```javascript
//App.js
import React from "react";
import BucketList from './BucketList';
import "./style.css";
import styled from "styled-components";

class App extends React.Component {
  constructor(props) {
    super(props);

    this.state = {
      list: ["옷이랑 신발사기", "하루동안 아무것도 안하기", "자전거 타기"],
    }
  }

  render() {
    console.log(this.state.list)
    return (
      <div className="App">
        <Container>
          <div className="container">
            <h1>내 버킷리스트</h1>
            <hr className="line" />
            <BucketList list={this.state.list}/>
          </div>
        </Container>
      </div>
    );
  }
}

const Container = styled.div`
  background-color: #eee;
  height: 100vh;
  width: 100vw;
  display: flex;

  .container {
    margin: auto;
    background-color: #fff;
    width: 50vw;
    max-width: 350px;
    height: 80vh;
    padding: 16px;
    border: 1px solid #ddd;
    border-radius: 5px;

    h1 {
      color: slateblue;
      text-align: center;
    }

    hr {
      margin: 16px 0px;
    }

    .list-item {
      padding: 16px;
      margin: 8px;
      background-color: aliceblue;
    }
  }
`;
//div.App은 잘 안건드리는 듯하다... 조심하자!
//변수명으로 태그를 변경해야 작동한다!
export default App;
```  

## 리액트 2주차 10강(Ref! 리액트에서 돔요소 가져오려면?)  
자바스크립트 시간에 배웠던 DOM 조작 방법은 리액트에 적합하지 않다.(가상돔이 진짜가 되었을 때만 건드릴 수 있기 때문에 부적합)  

1. return jsx에 input태그 추가
2. 클래스형으로 작성되었을 때 constructor에 this.text = React.createRef(); 생성  
3. componentDidMount(){...}로 실제 돔에 마운트 되었는지 체크
4. this.text.current.value; + onChange={...}로 현재값 가져올 수 있음 
5. BucketList.js같은 함수형으로 작성된 파일에선 Ref값을 React Hook을 사용해 가져올 수 있다.

## 리액트 2주차 11강(State관리1 : 클래스 컴포넌트 관리)  
단방향 데이터 흐름: 부모에서 자식으로 데이터를 수정  
수정하게 될 때 문제발생: 자식이 부모에게 데이터 영향을 주는 상황이 발생하면 무한 렌더링이 발생하게 된다(상황에 따라 발생하지 않을 수도 있음).  
때문에 단방향 데이터 흐름을 사용한다.  

리액트에서는 유니크한 키값을 가져야한다.
```javascript
import React from "react";

class App extends React.Component {
  constructor(props) {
    super(props);

    this.state = {
      count: 3,
    };
  }

  componentDidMount() {}

  addNemo = () => {
    this.setState({count: this.state.count + 1})
  }

  removeNemo = () => {
    if(this.state.count > 0) {
      this.setState({count: this.state.count - 1})
    } else {
      window.alert("네모가 없어요!");
    }
  }

  render() {
    const nemo_count = Array.from({length: this.state.count}, (v, i) => i + 1);

    console.log(this.state);
    return (
      <div className="App">
        {nemo_count.map((i) => {
          return <div
          key={i}
          style={{
            width: "150px",
            height: "150px",
            backgroundColor: "#ddd",
            margin: "10px",
          }}>
            nemo
          </div>
        })}
        <div>
          <button onClick={this.addNemo}>하나 추가</button>
          <button onClick={this.removeNemo}>하나 빼기</button>
        </div>
      </div>
    );
  }
}
//Array.from 활용법 mdn 다시 보기
//return div의 key값 잘 봐둘 것
//함수 선언시 const 나 let 필요없음
//this.addNemo() this.removeNemo()는 즉시 실행이라는 뜻! 주의하자
export default App;
```
## 리액트 2주차 11강(State관리2: 함수형 컴포넌트 관리)  
```javascript
import React from "react";


const Nemo = (props) => {
    const [count, setCount] = React.useState(3);
    console.log(count);
    const nemo_count = Array.from({length: count}, (v, i) => i);

    const addNemo = () => {
        setCount(count + 1);
    };

    const removeNemo = () => {
        if (count > 0) {
            setCount(count -1)
        } else {
            alert("더이상 네모가 엄서요!")
        }
    };
    return (
        <>
        {nemo_count.map((i) => {
            return <div
            key={i}
            style={{
              width: "150px",
              height: "150px",
              backgroundColor: "#ddd",
              margin: "10px",
            }}>
              nemo
            </div>
          })}
          <div>
            <button onClick={addNemo}>하나 추가</button>
            <button onClick={removeNemo}>하나 빼기</button>
          </div>
        </>
    );
};
//return시 빈 태그로 하나로 묶어줘야 함
//함수 선언시 const 나 let 으로 선언
// 이전 강의인 클래스형 컴포넌트와 비교해가며 볼 것
export default Nemo;
``` 
중요)  
export import는 뼈대 불러오기(중심이 되는 App에서 부른다. 얼핏보면 하위에서 상위로 보내주는 것 같지만 props랑 다른 느낌!!!)  
정보를 내려주는건 상위에서 하위로만(상관있음, App에서 Name으로 props 내려주기 가능하지만 반대는 불가능)  
이 느낌에 익숙해지자

#### 일기
12시가 지났지만 2주차를 끝냈다! 장하다 내 자신!!