# 항해 20일차

## 리액트2 3주차 1강(3주차 오늘 배울 것)  

## 리액트2 3주차 2강(포스트 목록 가져오기)  
post.js reducer 작성, initialState, initialPost 만들어서 PostList에서 불러오기(아직은 빈 배열)

이러한 기능을 만들 때는 어떤 데이터가 필요하고, CRUD 시 어떻게 변하는지 생각하면서 하는 것이 중요!

## 리액트2 3주차 3강(파이어스토어 연동하기)  

파이어 스토어 인증 문제  
```javascript
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /{document=**} {
      // allow read, write: if false;
       allow read, write: if request.time < timestamp.date(2021, 11, 23);
    }
  }
}
```
인증 문제가 발생해서 권한을 타임스탬프로 주었더니 잘 되었다.

reduce정리  

https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce
```javascript
//파이어스토어에서 뽑아낸 doc
let _post = doc.data();

doc.data() = {
    user_id: "test",
    user_name: "Dongwoo",
    user_profile: pepe,
    image_url: pepe,
    contents: "페페네요!",
    comment_cnt: 10,
    insert_dt: "2021-09-30 16:00:00",
}


let post = Object.keys(_post).reduce((acc, cur) => {
    if (cur.indexOf("user_") !== -1) {
        return { ...acc, user_info: { ...acc.user_info, [cur]: _post[cur] } };
    }

    return { ...acc, [cur]: _post[cur] }
}, { id: doc.id, user_info: {} });

//결과 포스트
const post = {
    id: 0,
    user_info: {
        user_id: "test",
        user_name: "Dongwoo",
        user_profile: pepe,
    },
    image_url: pepe,
    contents: "페페네요!",
    comment_cnt: 10,
    insert_dt: "2021-09-30 16:00:00",
}
```
왜 reduce를 쓸까: 수작업을 쓰지않고 깔끔하게 결과 포스트를 만들려고!

1. Object.keys(대상 오브젝트)를 사용해 ['comment_cnt', 'contents', ...] 오브젝트의 키 값만 배열로 만든다.
2. 키 배열에 reduce를 돌린다. 이 때 기본값은 배열에 존재하지 않는 doc.id와 user_info가 된다.
3. 해당 키값에서 user_info와 관련된 값인지 체크한다.
3. 만약 해당이 된다면 user_info 안에 값을 넣고 리턴한다. 이 값은 acc가 된다.
3. 만약 해당이 되지 않는다면 그 밖에다가 값을 넣는다. 이 값은 acc가 된다.
4. 다음 키값으로 넘어간다.
5. 이후 반복할 때 스프레드 문법을 통해 중복되는 부분은 지워지기 때문에(예를 들어 ...acc에 user_info가 이미 들어가는데 다시 if문에서 user_info를 설정하는 것 등) 중복되지 않고 원하는대로 정리된 새 오브젝트가 post가 된다.

## 리액트2 3주차 4강(포스트 작성하기)  
history.replace() 새 페이지로 가는 것이 아니라 현재 페이지를 바꾸는 것. 뒤로가기 했을 때 원하지 않는 페이지가 다시 나오는 것 방지.

## 리액트2 3주차 5강(포스트 작성하기2)  
자바스크립트 패키지 모멘트: 시간을 쉽게 다룰 수 있다.

## 리액트2 3주차 6강(firebase Storage1)  
파이어 스토어와 javascript 파일 설정을 통해 파일 업로드를 한당

## 리액트2 3주차 7강(firebase Storage2)  

## 리액트2 3주차 8강(preview 만들기)  
https://developer.mozilla.org/ko/docs/Web/API/FileReader

## 리액트2 3주차 9강(게시글 작성 시 이미지 업로드)  

## 리액트2 3주차 10강(Debounce와 Throttle)
너무 많은 이벤트가 발생할 때 일정시간 이후 이벤트 수행(debounce), 이벤트를 모아서 주기적으로 1번 실행(throttle)  

기능이 다르므로 상황에 맞게 사용한다.

## 리액트2 3주차 10강(lodash로 이벤트 관리하기 - debounce, throttle)  
함수형 컴포넌트가 리렌더링 될 때 컴포넌트 안의 함수들도 초기화가 된다. 즉 디바운스 스로틀이 먹히지 않는다. => 이를 방지하기 위해 useCallback Hook 사용 이 훅은 지정한 함수를 따로 지정하여 리렌더링이 되어도 초기화 되지 않게 한다!(⭐) 최적화 할 때 굉장히 중요한 hook

Permit header 회원가입 후 페이지 이동 시 새로고침 하고 다시 로그인 해야 제대로 작동함
