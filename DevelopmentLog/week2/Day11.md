# 항해 11일차

## 흐름 정리(최신 기술 적용 기준)  
컴포넌트
* App.js가 메인이 된다. 다른 기능별로 파일로 빼서 새로운 컴포넌트를 만들 수 있다.  

스타일링  
* styled-components 패키지를 활용해 js에서 바로 스타일링 적용가능  


라우팅  
* react-router-dom 패키지를 활용한다.
* 페어지가 넘어가는 효과(url변경, 컴포넌트 교체) 등이 발생하게 해준다.
* index.js에서 BrowerRouter 태그 걸기
* 이동을 원하는 컴포넌트마다 Route 태그 걸기
* 원하지 않는 페이지 이동을 막기위해 Switch 태그와 NotFound 컴포넌트로 묶어주기  

리덕스  
* 이전에 State와 Props로 내려받던 data들을 전부 redux라는 전역상태 저장소에 넣고 편하게 사용하는 것 이 목표
* react-redux 패키지 활용  

기본 작업
* redux 폴더 생성 
    * 버킷리스트와 관련된 데이터, action, actioncreator, reducer를 저장하는 bucket.js 파일을 modules 폴더에 저장
    * bucket.js에서 리듀서들을 모으고 필요하면 추가적인 요소들도 합쳐 스토어로 만든 파일을 configStore.js로 저장  

사용 시  
* hooks인 useDispatch와 useSelector 활용  
    * 저장소 => 컴포넌트로 데이터 가져오고 싶을 때  
    useSelector((state) => {state.데이터})  
    여기서 state는 리덕스 스토어가 가진 전체 데이터  
    * 컴포넌트 => 저장소로 데이터 변경하고 싶을 때  
    useDispatch(액션크리에이터(변경하고 싶은 내용)) => 액션크리에이터 타고 => 리듀서에서 새 배열 만들고 새 배열 리턴  
    ![액션크리에이터의 내용](/images/react_week3/6.PNG)  
    그래서 리듀서에서 action.bucket 이런식으로 접근하는 것이다.  
    * 주의! 받아와지는 값은 전부 문자열이다("1", "text") 숫자 문자 관계없이. 이 점 주의할 것 

## 리액트 3주차 13강(숙제)
~~1. App.js에 Container 만들고 스타일링(styled-components)~~  

~~2. Route~~  

일단 성공!!  
돌아가기 버튼 누르면 정보 다시 리셋되는거 구현 못함...
정리하기에 너무 많다... 어떻게 해야할지 고민을 해보자!  

## 리액트 4주차 1강(keyframes)

css 화면전환:  
* transition  
    화면이 두 배 커진다고 할 때 일정한 속도로 늘어난다.
* animation  
    화면이 두 배 커진다고 할 때 처음엔 천천히 나중엔 빠르게 늘어나도록 속도 조절을 할 수 있게 해준다.  

애니메이션 효과에서 이 속도를 조절할 수 있게 해주는 요소(규칙)를 keyframes라고 한다.  
```javascript
import styled, {keyframes} from "styled-components";

function App() {
  return (
    <div className="App">
      <Box></Box>
    </div>
  );
}

const boxAnimation = keyframes`
  0% {
    border-radius: 0%;
    top: 20px;
    left: 20px;
  }
  25% {
    top: 300px;
    left: 300px;
  }
  50% {
    border-radius: 25%;
    top: 700px;
    left: 700px;
  }
  75% {
    border-radius: 25%;
    top: 100px;
    left: 100px;
  }
  100% {
    border-radius: 50%;
    top: 300px;
    left: 300px;
  }
`;

const Box = styled.div`
  width: 100px;
  height: 100px;
  background: green;
  border-radius: 50%;
  position: absolute;
  top: 20px;
  left: 20px;
  animation: ${boxAnimation} 2s 1s infinite linear alternate
`;

//왔다리 갔다리ㅋㅋㅋ
export default App;
```
## 리액트 4주차 2강(버킷리스트에 프로그래스바 달기)

데이터 수정, bucket에 액션 / 액션생성함수 / 리듀서 추가, 디스패치

transition이랑 섞어서 progress바 효과 내기

## 리액트 4주차 3강(스크롤바 움직이기)  
window.scrollTo({top, left, behaivor}) 줘서 스크롤 최상단으로 가게  

## 리액트 4주차 4강(Quiz_버킷리스트 좀 더 예쁘게!)  
 ```javascript
//Progress.js 포인터
const Pointer = styled.div`
    width: 37px;
    height: 37px;
    background: orange;
    border-radius: 50%;
    border: 3px solid black;
    margin: 0px -10px;
    flex-shrink: 0;
`;
//포인터 왼쪽으로 살짝 움직이고 싶을 때 마진 마이너스로 줄 것!
```

```javascript
//App.js 검색창
const Input = styled.div`
max-width: 350px;
min-height: 10vh;
background-color: #fff;
padding: 16px;
margin: 20px auto;
border-radius: 5px;
border: 1px solid #ddd;
display: flex;
flex-direction: column;
justify-content: center;
& input {
    border: 1px solid gray;
    margin-bottom: 10px;
}

& input:focus {
    outline:none;
    border: 2px solid orange;
    transition: 2s;
}
`;

//& 하위 컴포넌트! 잊지말 것
```  

## 리액트 4주차 5강(Firebase란?)  
![서버가 하는 일](/images/react_week4/1.png)  

파이어스토어는 BaaS(Backend as a Service)이며, 데이터 베이서, 소셜 서비스 연동, 파일시스템 등을 API 형태로 제공해준다.

## 리액트 4주차 6강(Firebase 설정하기)

## 리액트 4주차 7강(Firestore 설정하기)  
cloud Firestore 위치: asia-northeast2  
React.useEffect 다시 찾아보기  

## 리액트 4주차 8강(React에 Firebase 연동하기)  
React.useEffect 다시 찾아보기 => 렌더링 이후에 어떤 일을 수행해야하는지 말한다, 문서지정, 데이터 가져오기, 명령형API를 부르는 데에 쓰인다.

## 리액트 4주차 9강(Firestore 데이터 가지고 놀기)  
통신은 비동기 => async, await 사용  
query의 forEach는 Array함수가 아닌 query객체만의 특별한 함수라고 생각하자!

#### 일기
내 맘대로 하고 싶지만 에러와 싸우기엔 시간이 너무 짧다....ㅠㅠㅠㅠㅠ 4주차 과제에서 막혔다. 원인은 리덕스 설계를 잘못한 것 같다. 내가 생각한거랑 구조가 완전 다르다. 근데 내 방법도 맞는 것 같은데 리액트가 타입을 읽어오지 못한다.  
> TypeError: Cannot read properties of undefined (reading 'current') 
찾아보니 불러올 때 생기는 문제인 것 같다. 으아 너무 어렵다 내일 다시 찬찬히 생각해보면서 강의를 봐야겠다.