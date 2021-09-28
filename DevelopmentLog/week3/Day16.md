# 항해 16일차  

## 오늘 할 일
S3로 배포  
팀원들과 프로젝트 복습하기  
컴포넌트 만들어보기

## 배운 것
* 호스팅
    다른 서버를 통해 내 웹페이지가 계속 작동할 수 있도록 해주는 서비스  
    개인적으로 파이어베이스 호스팅이 좀 더 편한 것 같아서 이 방법으로 제출을 했다.

* 라이프 사이클
    컴포넌트가 생성되고 사라지는 주기를 표현, 클래스형 컴포넌트에서 함수로 이루어져 있으며, 각 요소는 어떤 상태에서 작동을 하는지 나타낸다.  
    https://ko.reactjs.org/docs/react-component.html#the-component-lifecycle  

    생성, 업데이트, 제거 순으로 진행된다.
  
![기본주차 끝](/images/react_week2/1.PNG) 

* 리액트 훅(React Hooks)  
    Hook은 React 버전 16.8부터 React 요소로 새로 추가되었습니다. Hook을 이용하여 기존 Class 바탕의 코드를 작성할 필요 없이 상태 값과 여러 React의 기능을 사용할 수 있습니다. 
    https://ko.reactjs.org/docs/hooks-reference.html#usestate

* 근데 Hook이 뭔가요?
    __Hook은 함수 컴포넌트에서 React state와 생명주기 기능(lifecycle features)을 “연동(hook into)“할 수 있게 해주는 함수입니다.__ (중요⭐⭐⭐) Hook은 class 안에서는 동작하지 않습니다. 대신 class 없이 React를 사용할 수 있게 해주는 것입니다. (하지만 이미 짜놓은 컴포넌트를 모조리 재작성하는 것은 권장하지 않습니다. 대신 새로 작성하는 컴포넌트부터는 Hook을 이용하시면 됩니다.)  

* useState();
    리액트 훅 중 하나로서 state와 prop을 쓸 수 있게(변수를 사용할 수 있게) 해준다. 컴포넌트 함수에는 this를 사용할 수 없기에 이런 방법을 사용한다.
    리렌더링 시 가장 최근에 갱신 된 값을 제공한다.  

```javascript
import React, { useState } from 'react';

  function Example() {
    const [count, setCount] = useState(0);

    return (
      <div>
        <p>You clicked {count} times</p>
        <button onClick={() => {
            setCount(count + 1);
            console.log({count}, {setCount});
            }}>
         Click me
        </button>
      </div>
    );
}

export default Example;
```

    const [count, setCount] = useState(0);  
    이런 식으로 사용되며, 변수1, 2에는 배열 구조 분해 방식이 적용되어 각각 0, 0의 값이 들어간다.  
    그러나 클릭을 할 때마다 변수 setCount의 값이 count(0) + 1 즉 1이 된다.
    다음 클릭 시에는 count가 setCount의 값을 감지해서 1이 되고 setCount는 + 1 해서 2가 되는 방식이다.  

![useState](/images/week3/1.png)

* useEffect  
    https://ko.reactjs.org/docs/hooks-effect.html  


## 일기  
아직 나는 많이 부족하다. 두번째 프로젝트를 시작했는데 손도 대지 못했다. 아직 훅의 개념을 정확히 잡지 못해 일어난 일이라고 생각해 리액트 공식문서를 읽어보았다. 역시 읽어보니 몰랐던 개념들이 많았다.  
useState는 값을 2개씩 묶어서 감시하는 역할이고, useEffect는 다른 함수나 데이터를 불러와서 리로드 될 때마다 실행시켜주는 역할을 한다는 것을 확실히 알게 되었다. 뒤에 의존성 배열은 배열 안에 있는 요소가 바뀔 때만 작동 시키게끔 하는(불필요한 리로드시 작동을 막기위해) 것이라는 것도 확실히 알게 되었다. 내일은 다시 한번 hook 개념과 canvas mdn 문서만 가지고 만들기 도전을 해봐야겠다! 