# 항해 10일차

## 리액트 3주차 1강(이벤트 리스너)  
이번주에 배울 것  

이전의 인터넷 환경에서는 API 요청을 하면 그에 해당하는 html 페이지를 주었다.  
그러나 리액트는 html페이지가 하나이다 => 라우팅을 사용해 문제 해결

리덕스: 전역상태관리를 해주는 엄청난 패키지!
![리덕스 적용 전](/images/react_week3/1.PNG)  

리덕스 적용 전에는 형제관계이거나 엄청 먼 자식 관계에서 상태(props)를 넘겨주려면 불가능하거나 불편한 과정을 거쳐야 한다.  

![리덕스 적용 후](/images/react_week3/2.PNG)  

리덕스 적용 후에는 리덕스 스토어라는 전역데이터 저장소에서 상태를 받아 사용할 수 있기 때문에 문제가 해결된다.  

이벤트 리스너?: 사용자가 어떤 행동을 했을 때 알려주는 것이다.  

클래스 컴포넌트에서 이벤트리스너 추가 및 삭제
```javascript
//App.js
import './App.css';
import React from "react";
import Text from "./Text";

class App extends React.Component{
constructor(props){
super(props);

this.state = {};
    this.circle = React.createRef(null);
}

hoverEvent = (e) => {
    console.log(e.target);
    console.log(this.circle.current);
    this.circle.current.style.background = "yellow";
}

componentDidMount() {
    console.log(this.circle);
    this.circle.current.addEventListener("mouseover", this.hoverEvent);
}

componentWillUnmount() {
    this.circle.current.removeEventListener("mouseover", this.hoverEvent);
}

//페이지의 생성 수정 삭제(라이프 사이클)에 맞는 함수에다 addEventListener와 removeEventListener를 작성한다.
//ref는 항상 ref.current로 접근할 것
render() {
return (
<div style={{width: "100vw", height:"100vh", textAlign:"center"}}>
<Text/>
<div style={{
    margin:"auto", 
    width: "250px", 
    height: "250px", 
    background:"green", 
    borderRadius:"250px"
    }} ref={this.circle}></div>

</div>
);
}
}

export default App;
```

```javascript
//Text.js
import React from "react";

const Text = (props) => {
const text = React.useRef(null);

const hoverEvent = () => {
    text.current.style.background = "yellow";
};
React.useEffect(() => {
    text.current.addEventListener("mouseover", hoverEvent);

    return () => {
        text.current.removeEventListener("mouseover", hoverEvent);
    }
}, []);

//함수형 컴포넌트는 페이지 생성, 수정, 삭제에 관련된 함수가 따로 없고, useEffect(() => {}, []); 라는 react hooks를 사용한다.

//생성, 수정, 삭제가 하나로 합쳐진 느낌이며, 생성은 첫번째 인자인 함수로, 삭제는 첫번째 인자 함수의 return 함수로, 수정은 두번째 인자(depencency array)에서 비교 대상을 넣는다. 

//그러면 처음(렌더링 시)엔 무조건 함수를 1회 실행하고, 그 다음부터 수정이 일어나면 두번째 인자를 비교하여 바뀐 부분만 함수가 발생하는 원리이다.

//왜 튜터님이 클래스 컴포넌트 방식을 같이 쓰시는지 이해가 갔다. 바로 useEffect로 설명했으면 이해하기 어려웠을 것이다.
return (
<h1 ref={text}>텍스트입니다!</h1>
)
}

export default Text;
```

## 리액트 3주차 2강(라우팅이란?)  

![기존의 페이지 이동](/images/react_week3/3.PNG)  

클라이언트에서 페이지 이동 요청을 하면, 그에 맞는 html파일을 서버가 주는 방식이 기존의 페이지 이동 방식이고, 이를 MPA 방식이라고 부른다.  
```python
@app.route('/')
    def home:
        return render_template('main.html')

@app.route('/mypage')
    def home:
        return render_template('mypage.html')

```
미니프로젝트(flask)에서 썼던 방식이라 생각하면 될 듯하다.  

![리액트의 페이지 이동](/images/react_week3/4.PNG)  
리액트에서는 실질적인 html파일의 교체는 없고 내용만 바뀐다!  

리액트(SPA)를 쓰는 가장 중요한 이유는 사용성 때문! 필요한 작업만  갈아준다, 다른 이유는 상태유지 때문이다. 예시로 회원가입 페이지에서 하나만 실수하면 리로딩 되면서 기존의 자료가 날라가는 경우가 있다. 이런 문제를 해결할 수 있다.  

단점은 한번에 모든 컴포넌트를 다 불러오기 때문에 시간이 걸린다.  

정리: 리액트에서 라우팅이란 모든 컴포넌트를 불러 필요한 페이지에 필요한 컴포넌트를 위치 시키는 것!  

react-route-dom 패키지를 이용할 계획이다.  

## 리액트 3주차 3강(리액트에서 라우팅 처리하기1)  

> (해당 프로젝트 폴더에서) yarn add react-router-dom  react-router

공식문서 : https://reactrouter.com/web/guides/primary-components  

## 리액트 3주차 4강(리액트에서 라우팅 처리하기2)  

index.js 에서 라우터 실행

동적 라우팅 : 바뀔수도 있는 라우팅
```javascript
//index.js
import React from 'react';
import ReactDOM from 'react-dom';
import './index.css';
import App from './App';
import reportWebVitals from './reportWebVitals';
import {BrowserRouter} from "react-router-dom";

ReactDOM.render(
  <BrowserRouter>
    <App />
  </BrowserRouter>,
  document.getElementById('root')
);

// If you want to start measuring performance in your app, pass a function
// to log results (for example: reportWebVitals(console.log))
// or send to an analytics endpoint. Learn more: https://bit.ly/CRA-vitals
reportWebVitals();
```
라우터 기본설정

```javascript
//App.js
import {Route, Link} from 'react-router-dom';
import Home from './Home';
import Cat from './Cat';
import Dog from './Dog';

function App() {
  return (
    <div className="App">
      <div>
        <Link to="/">Home으로 가기</Link>
        <Link to="/cat">Cat으로 가기</Link>
        <Link to="/dog">Dog으로 가기</Link>
      </div>
      <Route path='/' exact>
        <Home />
      </Route>

      <Route path='/cat' component={Cat}>
        {/* <Cat /> */}
      </Route>

      <Route path='/dog'>
        <Dog />
      </Route>

    </div>
  );
}

export default App;
```
App.js에서 Route로 경로 지정, props를 쓰는 방법과 reactHook을 쓰는 방법이 있다. 둘 중 편한거 골라쓰면 됨.

```javascript
//Home.js
import React from 'react';

const Home = (props) => {
    return (<div>메인 화면입니다!</div>);
};

export default Home;
```

```javascript
//Cat.js
import React from 'react';
import {useParams} from 'react-router-dom';

const Cat = (props) => {
    // const cat_name = useParams();
    // console.log(cat_name);
    console.log(props);
    return (<div>고양이 화면입니다!</div>);
};

export default Cat;
```

```javascript
//Dog.js
import React from 'react';
import { useHistory } from 'react-router';
const Dog = (props) => {
    const history = useHistory();
    console.log(props);
    return (<div onClick={() => {
        history.push("/cat")
    }}>강아지 화면입니다!</div>);
};

export default Dog;
```  
이 중에서 하나만 골라서 써보고 적응되면 다른 방식도 써보는 것을 튜터님은 추천하셨따. 아마 reactHooks로 통일해서 써볼듯?

## 리액트 3주차 5강(Quiz_버킷리스트 상세페이지 만들고 이동하기)  
```javascript
//1.index.js 라우터 작업
import React from 'react';
import ReactDOM from 'react-dom';
import './index.css';
import App from './App';
import reportWebVitals from './reportWebVitals';
import {BrowserRouter} from "react-router-dom";

ReactDOM.render(
  <BrowserRouter>
    <App />
  </BrowserRouter>,
  document.getElementById('root')
);

// If you want to start measuring performance in your app, pass a function
// to log results (for example: reportWebVitals(console.log))
// or send to an analytics endpoint. Learn more: https://bit.ly/CRA-vitals
reportWebVitals();
```

```javascript
//2. App.js 필요한 컴포넌트 마다 라우트 시키기
import React from "react";
import styled from "styled-components";
import { Route } from "react-router-dom"; 
// BucketList 컴포넌트를 import 해옵니다.
// import [컴포넌트 명] from [컴포넌트가 있는 파일경로];
import BucketList from "./BucketList";
import Detail from "./Detail";

function App() {

const [list, setList] = React.useState(["영화관 가기", "매일 책읽기", "수영 배우기"]);
const text = React.useRef(null);

const addBucketList = () => {
// 스프레드 문법! 기억하고 계신가요? :) 
// 원본 배열 list에 새로운 요소를 추가해주었습니다.
setList([...list, text.current.value]);
}
return (
<div className="App">
<Container>
<Title>내 버킷리스트</Title>
<Line />
{/* 컴포넌트를 넣어줍니다. */}
{/* <컴포넌트 명 [props 명]={넘겨줄 것(리스트, 문자열, 숫자, ...)}/> */}
<Route path="/" exact>
    <BucketList list={list}/>
</Route>
<Route path="/detail" exact component={Detail}>
</Route>
</Container>
{/* 인풋박스와 추가하기 버튼을 넣어줬어요. */}
<Input>
<input type="text" ref={text} />
<button onClick={addBucketList}>추가하기</button>
</Input>
</div>
);
}

//...css 생략
export default App;
```

```javascript
//3. BucketList.js 에 useHistory hooks 이용하여 onClick 함수에 라우팅 넣어주기
import React from "react";
import styled from "styled-components";
import { useHistory } from "react-router";

const BucketList = (props) => {
const history = useHistory();
// console.log(props, history);
const my_lists = props.list;

return (
<ListStyle>
{my_lists.map((list, index) => {
return (
<ItemStyle className="list_item" key={index} onClick={() => {
    history.push("/detail");
}}>
{list}
</ItemStyle>
);
})}
</ListStyle>
);
};
//...css생략
export default BucketList;
```

```javascript
//4. Detail.js 에 useHistory hooks 이용하여 onClick 함수에 라우팅 넣어주기
import React from 'react';
import { useHistory } from 'react-router';

const Detail = () => {
    const history = useHistory();
    return (
        <h1 onClick={() => {
            history.push("/");
        }}>상세페이지 입니다!</h1>
    );
};

export default Detail
```

## 리액트 3주차 6강(라우팅, 조금 더 꼼꼼히 쓰려면?)  
잘못된 주소 처리하기  
> /12341234같은 아예 잘못된 주소로 접근할 때 처리  
라우터에서 Switch 불러온 다음 Route 부모태그로 걸면 Route가 일치하는 곳에서 멈추고, 일치하지 않으면 path지정을 하지 않은 곳으로 보낸다.  

```javascript
//1. App.js Switch를 불러서 Route 부모태그로 위치시킨다.
import React from "react";
import styled from "styled-components";
import { Route, Switch } from "react-router-dom"; 
import BucketList from "./BucketList";
import Detail from "./Detail";
import NotFound from "./NotFound"

function App() {

const [list, setList] = React.useState(["영화관 가기", "매일 책읽기", "수영 배우기"]);
const text = React.useRef(null);

const addBucketList = () => {
setList([...list, text.current.value]);
}
return (
<div className="App">
<Container>
<Title>내 버킷리스트</Title>
<Line />
{/* 컴포넌트를 넣어줍니다. */}
{/* <컴포넌트 명 [props 명]={넘겨줄 것(리스트, 문자열, 숫자, ...)}/> */}
<Switch>
    <Route path="/" exact>
        <BucketList list={list}/>
    </Route>
    <Route path="/detail" exact component={Detail}>
    </Route>
    <Route>
        <NotFound />
    </Route>
</Switch>
</Container>
{/* 인풋박스와 추가하기 버튼을 넣어줬어요. */}
<Input>
<input type="text" ref={text} />
<button onClick={addBucketList}>추가하기</button>
</Input>
</div>
);
}
//...css 생략

export default App;
```

```javascript
//2. NotFound.js
import React from "react";
import { useHistory } from "react-router-dom";

const NotFound = () => {
    const history = useHistory();
    return (
        <>
            <h1>주소가 올바르지 않다요!</h1>
            <button onClick={() => {
                history.push("/");
            }}>뒤로가기</button>
        </>
    );
};

export default NotFound;
```
## 리액트 3주차 7강(리덕스란?)  
리덕스: 전역상태 저장소  
버켓리스트 예시:  

현재상태에서 추가하기 컴포넌트는 App.js에 있고, 버킷리스트 state도 App.js 안에 있다.  
  
추가하기 컴포넌트를 Add.js라는 파일로 분리해서 App.js에서 import 했다고 하자.  
  
이 때 추가버튼을 누르면 하위 컴포넌트인 Add.js에서 App.js를 수정하게 되는 원래 흐름과 반대로 가게된다.  

이럴 때 상태관리가 아주 유용하다.  

Add.js의 추가버튼을 눌렀을 때 전역 변수를 바꾸어 부모 컴포넌트의 state를 바꾸지 않고 변경할 수 있다.  

또한 자식 컴포넌트가 100개쯤 있는 App.js가 있다면, 100번째 상태를 변경하기 위해서 다른 곳에도 필요없어도 props를 99번 내려줘야 하는데, 이것 또한 비효율적이기 때문에 상태관리를 사용하여 관리한다.(props drilling 문제 해결)  

![리덕스 구조](/images/react_week3/5.png)  
1. 전역적으로 데이터(state)를 관리하는 친구가 있다.
2. 이 데이터(state)를 참조하거나 수정하고 싶은 친구(컴포넌트)들도 있다.  
3. 바뀐 값을 모두가 볼 수 있게 해줘야 한다.

* 스토어: 전역 데이터(state)가 저장되어있는 장소, 리듀서들의 집합  
* 리듀서: 데이터(state)를 실제로 수정하는 공간
* 구독: 데이터(state)를 받아가는 행위(스토어와 컴포넌트가 연결되어있음)  
* 액션을 디스패치: 녹색 컴포넌트에서 특정 데이터(state) 값을 변경하려는 행위, 리듀서를 거쳐 스토어가 변경되면 변경되었다는 걸 구독한 컴포넌트에게 알리고 리렌더링 발생   

## 리액트 3주차 8강(리덕스를 통한 리액트 상태관리)

## 리액트 3주차 9강(리덕스 써보기)
덕스🦆(ducks) 구조:  
기능으로 묶어서 사용하자는 방법론  
예를 들어 버킷리스트 => 버킷리스트의 action actionCreator, reducer를 한 파일에 넣어놓는 것.
> yarn add redux react-redux

```javascript
//모듈 만들기 위치: /src - /redux - /modules - bucket.js
// bucket.js

// Actions
const CREATE = 'bucket/CREATE';
//프로젝트 이름/리듀서(모듈)/액션 , 액션 타입을 만들어 주는 곳


const initialState = {
    list: ["영화관 가기", "매일 책읽기", "수영 배우기"],
};
//시작값 만들어 놓기

// Action Creators
export function createBucket(bucket) {
    return { type: CREATE, bucket: bucket };
    //{bucket: bucket} 일 때 {bucket} 으로 줄여 쓸 수 있다.
}
//액션 생성 함수 작성

// Reducer
export default function reducer(state = initialState, action = {}) {
//변수에 혹시라도 값이 안 들어왔을 때를 대비해 빈 Object로 기본 변수 값 지정
    switch (action.type) {
    // do reducer stuff
    case "bucket/CREATE": {
        const new_bucket_list = [...state.list, action.bucket];
        return {list: new_bucket_list};
    }
    default: 
        return state;
    }
}
//state 변경해주는 부분
```

```javascript
//configStore.js 위치: /src - /redux - configStore.js
import {createStore, combineReducers} from 'redux';
import bucket from "./modules/bucket";

const rootReducer = combineReducers({bucket});
//리듀서 모으기

const store = createStore(rootReducer);

export default store;
//스토어는 리듀서들 + @의 집합이기 때문에 여기서 combineReducer로 합치고, createStore로 스토어 생성한다.
```
## 리액트 3주차 10강(리덕스와 컴포넌트를 연결하자!)  
이전 강의에서 생성한 store를 index.js에 넣어준다.  
```javascript
import React from 'react';
import ReactDOM from 'react-dom';
import './index.css';
import App from './App';
import reportWebVitals from './reportWebVitals';
import {BrowserRouter} from "react-router-dom";
import {Provider} from "react-redux";
//라우트 처럼 프로바이더 태그를 제일 바깥에 배치해준다.
import store from "./redux/configStore";
//만들어 둔 스토어를 프로바이더에 추가한다.

ReactDOM.render(
<Provider store={store}>
  <BrowserRouter>
    <App />
  </BrowserRouter>
</Provider>,
  document.getElementById('root')
);

reportWebVitals();
```

## 리액트 3주차 11강(컴포넌트에서 리덕스 데이터 사용하기)  
리덕스 훅: 함수형 컴포넌트처럼 리덕스도 훅이 있다.  
이 중 useDispatch는 데이터 업데이트 시,  
useSelector는 데이터를 가져올 때 사용한다.  

수정한게 너무 많다;; 나중에 다시 볼 것! 중요한 것은 props를 변수로 쓰는것이 아니라 useDispatch와 useSelector를 import해서 쓰는 것이다.

## 리액트 3주차 12강(Quiz_버킷리스트 데이터 삭제)  
filter 쓸때 parseInt(action.bucket_index) 여기서 작동이 안됐던 것 같다. 스트링으로 번호가 나오나보다... 정답 확인결과 맞았다! 이것 때문에 해맸다😥

#### 일기
리액트는 SPA를 만들기 쉽게 도와주는 도구지 Javascript를 대체 할만한 어떤 엄청난 도구가 아님을 조금씩 알아가고 있다. 이 도구를 언제 사용하는지, 어떤 개념을 사용하는지 이해하는 것이 중요한 것 같다. 듣는 양이 많다보니 가물가물 한데 흐름만 조금 잡힌 것 같은 느낌이다. 1회차 끝내고 코드 많이 짜면서 2회차 들어봐야겠다.  

오늘 안에 도저히 숙제를 못끝낼 것 같아 내일아침 다시 정리해보고 숙제를 좀 하려고 한다. 너무 아쉽다....😭 내일은 좀 더 집중을 잘 해보자!