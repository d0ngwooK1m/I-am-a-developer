# 항해 32일차

## 오늘 한 일

axios.interceptors로 쿠키 정보 넣기 => 인터셉트는 성공했으나 Unauthorize 에러가 계속 뜬다.
백엔드 문제였던걸로...ㅎㅎ user 값만 넣어주니깐 잘 된다!
https://axios-http.com/docs/interceptors  
https://jodev.kr/entry/React-axios%EB%A5%BC-%EC%82%AC%EC%9A%A9%ED%95%98%EC%97%AC-%ED%86%A0%ED%81%B0-%EA%B0%B1%EC%8B%A0-%ED%9B%84-%ED%97%A4%EB%8D%94%EB%A5%BC-%EB%B3%80%EA%B2%BD%ED%95%98%EB%8A%94-%EB%B0%A9%EB%B2%95

인풋 파라미터 바꾸기  
setState를 통해 input value 문제 해결 각 인풋에 하나씩 주는 것으로 구현했다.

저장 누르면 바로 갱신  
useEffect로 감지해 그 안의 값을 initialState의 값으로 변경해주어 사용성을 고려하였다.

url값에 ${}로 날짜 값 주기  
App.js 의 Route를 /main/:date로 주고 로그인 시 moment로 설정한 오늘 값을 date에 주는 것으로 구현했다.

왜 에러 핸들링을 하는가?:  
실질적으로 페이지 이동이 아니라 페이지 이동한 시점에서! axios 통신이 발생했을 때 에러코드를 주는 것이다! 그래서 페이지 이동 후 get 통신의 에러값이 401로 콘솔에 떴던 것이다~
정리하자면 페이지 이동을 막거나 하려면 에러 핸들링으로 다시 밀어주던지 할 필요가 있다!
에러 핸들링의 history는 useHistory가 아니라 configureStore.js의 export const history = createBrowserHistory(); 이다! 주의할 것

날짜 불러오기:  
날짜 불러오기를 리덕스를 써서 했다. 그 방법 밖에 생각이 안 나긴 했는데 더 좋은 방법이 분명 있을 것이다. 고민해 볼 것

## 내일 할 일

1. 아무 정보 없는 과거로 갈 시 선택 못하게 에러 핸들링
2. 마이페이지 작성
3. 상세 디자인 및 버튼 로그아웃 작성

## 일기

오늘 정말 많은 일을 했다! 끝까지 해서 메인페이지 완성까지 한 우리팀 나이서😎
