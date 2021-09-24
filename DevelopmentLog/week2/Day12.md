# 항해 11일차

## 4주차 숙제  
랭킹 화면에서 오류가 났던 이유  
1. updateRank 함수에서 변수를 2개 받아옴, 오브젝트 하나만 받아오는건데... 그래서 오류 발생(cannot read 오류는 그 때문인듯 하다.)  

2. 문제는 useRef였다. 랭킹화면에서 콘솔창에 참조를 해야한다는 경고창이 떠서 알아보니 나는 순위에 index+1을 매기고 있었는데 그렇게 하는 것이 아니라 const Id = useRef(0) 으로 지정해서 Ref={Id}로 태그에서 참조를 한 다음, Id.current + 1로 순위를 매겨주니 오류가 사라졌다. 참조를 어떻게 할지 고민하는 것도 중요한 것 같다.  

3. 프로그레스 바 문제가 있다. props로 정보 내려서 하는 것 까진 좋았는데 5/5 부분에서 그냥 넘어가버린다. 어떻게 해결할 수 있을지 고민해봐야겠다.

## 리액트 5주차 1강(리덕스에서 Firestore 데이터 가지고 놀기1)  
리덕스와 파이어베이스 통신은 비동기로 처리된다.   
정보들을 어디서 불러올까? => 미들웨어!  
![미들웨어가 하는 일](/images/react_week5/1.PNG)  
디스패치로 정보가 전송되고 reducer가 작동하기 전에 미리 작업을 해 놓는 녀석(?)  
액션 발생 => 미들웨어가 할 일 하기 => 리듀서에서 처리  

우리가 설치한 redux-thunk는 뭐하는 녀석인가?  
객체대신 함수를 반환하는 액션 생성함수를 만들게 해준다. 즉, 결과값이 함수로 나오게 되기 때문에 객체에 작업을 처리할 수 있게 된다.  

## 리액트 5주차 2강(리덕스에서 Firestore 데이터 가지고 놀기2)  
1시간짜리 강의 뭐임!😨  
비동기 통신: 시작되는 함수에 async 결과 값 또는 함수에 await => 없으면 결과값이 Promise로 나옴!  
파이어스토어 데이터 접근시 .data()로 접근해야 우리에게 필요한 데이터 형태로 접근 가능하다.
수정 및 삭제에는 데이터 id가 필요하다.  

cannot read property 오류가 나면  
삼항 연산자로  
> bucket_list[bucket_index]? bucket_list[bucket_index].text : ""  

요점은 리덕스 작업시 미들웨어로 중간에서 파이어베이스 DB작업을 하고(리덕스 DB와 같아야 하니깐) 완료가 되면 리덕스 리듀서가 작동하게 한다.  

이전 작업: 액션 및 액션 크리에이터 => 리듀서  
이후 작업 액션 및 액션 크리에이터 => 청크를 통한 미들웨어 작업 => 리듀서  

## 리액트 5주차 3강(머테리얼 UI 사용하기)  
와! 머테리얼 UI 아시는구나!

## 리액트 5주차 3강(페이지 의도적으로 가리기) 
로딩스피너 만들기... 그래도 스피너는 돈다...  
object 스프레드 사용하면 뒤에 있는 중복부분이 새 데이터가 된다(bucket.js)

#### 일기  
내일 할 일: 액션 - 파이어베이스(미들웨어) - 리듀서 프로젝트 실행할 수 있게끔 정리할 것.  
퀴즈 문제는 파이어스토어로 저장 안해도 될 것 같은데... 값이 변경 안되니까? 이게 맞는 건지 물어봐야겠다 그리고 로딩화면은 필요 없을 것 같다.  
뭔가 시원하진 않지만 그래도 5주차 다 들었다! 내일 배포하고 프로젝트 시작해봐야징