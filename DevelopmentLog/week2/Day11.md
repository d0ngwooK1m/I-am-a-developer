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
1. App.js에 Container 만들고 스타일링(styled-components)
2. Route  


    