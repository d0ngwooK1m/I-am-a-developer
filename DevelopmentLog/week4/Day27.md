# 항해 27일차  

## W.A 내가 찾은 답
1. s3 버킷에 배포한 뒤, 어떤도메인.com이 아닌 어떤도메인.com/login 등 페이지로 이동하면 왜 오류가 날까요?
    검색 결과 : 실제 route는 index.html 하나이기 때문에, 파일이 없다고 오류를 내는 것(Route는 React-Router-Dom에 의해 사용 가능) s3 설정시 index문서와 오류문서를 index.html로 해놓으면 오류가 나도 index.html로 가면서 React-Router-Dom의 라우팅을 탈 수 있게 된다. 
    https://leonkong.cc/posts/til-react-router-s3-cloudfront.html  



2. 리액트에서 각 페이지 컨텐츠에 맞는 미리보기(사이트 이미지, 사이트 설명 등)를 띄워주려면 어떻게 해야할까요?  

    내 생각: og 태그 활용한다. 

    검색결과: react-helmet 패키지를 받아 helmet 태그로 og태그에 필요한 정보를 넣으면 렌더시 헤더에 미리보기 정보가 들어간다.

    튜터님 답변:  
    메타태그를 페이지에 맞게 조절해준다. 그리고 검색봇이 해당 메타태그를 미리 읽어갈 수 있도록 서버사이드 렌더링 처리 혹은 pre-rendering처리 해준다.  
    더 알아보면 좋을 키워드 : SSR

3. 리덕스에서 미들웨어 청크의 역할은 뭘까요?  
    내 생각: ??? 미들웨어?  

    검색결과: 리덕스에서 비동기 접근, 웹 요청, 저장소 접근 등이 가능하게 해주는 미들웨어(어떠한 기능에서 중간다리 역할을 하는 것)다.  

    튜터님 답변:  
    액션 객체를 dispatch하는 대신 함수를 dispatch할 수 있도록 해준다. dispatch한 함수는 dispatch, getState, 그 외의 직접 설정한 값을 받아 사용할 수 있다.  
    비동기 처리 등에 사용할 수 있다.

4. 프로미스는 정확히 말하면 비동기가 아닙니다. 비동기와 프로미스는 각각 무엇일까요?  

    내 생각: 비동기는 작업 하나가 비동기 실행 될 동안 다른 작업을 진행하는 것이고, 프로미스는 비동기 작업이 실행 될 때까지 다른 작업이 대기하고 있는 것. 프로미스가 더 안전하다고 볼 수 있다.

    강의자료: 비동기는 정확한 종료시간을 알 수 없다. 프로미스를 사용하면 비동기 작업의 상황(시작, 진행, 종료)를 알 수 있다. + async, await 더 엄격하게 끝내야 진행  

    튜터님 답변:  
    1. 비동기는 요청을 보내고 해당 요청에 대한 응답을 기다리는 대신 다음 동작을 실행하는 방식.
    2. 프로미스는 비동기 처리에 사용되는 객체. (비동기 자체는 아니다.)

5. TDZ(Temporal Dead Zone/일시적 사각지대)란?

    내 생각: 기존 렌더링에서 재렌더링이 완료 될 때 까지 비는 시간

    동윤님 답변: 선언,초기화,할당 ///// 스코프의 선언 지점부터 초기화 시작 지점까지 사각지대.///// let과 const는 var와는 다르게 선언단계와 초기화 단계가 따로 분리되어 실행됨. 그래서 선언 단계와 초기화 단계 사이에서는 실행 컨텍스트에는 변수를 등록했지만 메모리가 할당되지 않은 상태라 `ReferenceError` 가 나옴. 이런 사각지대를 TDZ라한다.  

    튜터님 답변:  
    const, let을 선언할 때 선언 -> 초기화 단계를 거친다. 런타임(파일을 한 줄 한 줄 실행하는 것) 이전에 선언되어 메모리에 한 자리를 차지하지만 초기화 단계가 아직 실행되지 않았기 때문에 해당 변수(상수)에 접근할 수는 없는 상태를 TDZ라고 한다.

6. useRef()와 useState()는 변수에 관련된 훅이다. 두 훅의 차이점은 무엇일까?
    검색 답변: useState는 값 변경시 재렌더링이 발생하고, useRef는 그렇지 않다.
    https://velog.io/@lyj-ooz/useState-useRef%EC%9D%98-%EC%B0%A8%EC%9D%B4

7. useEffect()는 언제 작동하는 걸까?
    내 답변: 기본적으로는 렌더링이 수행되었을 때, 그러나 의존성 배열이 있다면 거기에 있는 값이 변경되었을 때만 작동하도록 할 수 있다.

## 발표 정리

오세명님 발표:  
멀티이미지 업로드 => map으로 jsx를 렌더링 하는 상황, 프로퍼티 속성 key로 idx를 주면 경고창이 뜨는 이유?
새로 idx구조가 변경되면서 새로 렌더링 되기 때문에 경고창을 띄운다. => key값을 고유id로 줌으로서 해결  

## 코드리뷰

하린님 코드에서 프론트에서 예상하지 못한 입력(제목 없음, 날짜 없음)에 대한 경고표시를 해주는 것을 잊었다. 디테일한 부분인데 앞으로 신경을 써야겠다.

