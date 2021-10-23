# 항해 40일차

toggle에 id 즉 고유값을 넣어줘야 하는데 그렇지 않아서 충돌이 일어난 것으로 보임. 시간이 남으면 postId와 commentId로 전부 대체할 것

## 이번에 하면서 아쉬웠던 점(김동우)

1. 컴포넌트 잘 쪼개기:

   문제가 어디서 발생했는가 : 작업이 진행되면 진행 될수록 디테일한 기능이 요구되고, 삼항 연산자들이 추가되면서 코드량이 걷잡을 수 없이 커져버렸다.

   문제 원인이 뭐라고 파악을 했는지 : 중간에 컴포넌트 분리를 하다가 오류로 인해 프로젝트가 지연될까 그대로 진행한 결과 Post.js코드는 600줄에 가까운 그야말로 스파게티 코드가 되고 말았다.

   문제 해결하기 위한 시도들 : 그대로 작업 강행

   어떻게 해결하는지 : 기능상 문제는 없었지만 나중에 코드를 알아보기가 아주 힘들었다.

   다음에는 이 문제를 발생시키지 않기 위해 어떻게 사전 작업할 것인지 : 1) 코드가 많아지고, 2) 작은 구조의 반복 이 발생하는 코드라면 즉시 컴포넌트를 쪼개는 식으로 작업을 진행해야겠다고 생각했다.

2. 스프레드 방식 useState에서 id 값을 제대로 주지 못한 점:

   문제가 어디서 발생했는가 : 연속한 댓글 삭제 시 댓글이 삭제되지 않고 화면이 고정되는 문제 발생

   문제 원인이 뭐라고 파악을 했는지 : map에 useState 적용 시 id 값을 map의 index로 사용 (id가 map의 영향을 받음)

   ```javascript
   const [shownCommentModal, setShownCommentModal] = React.useState({});
   const toggleCommentDelete = (id) => {
     setShownCommentModal((prevShownCommentModals) => ({
       ...prevShownCommentModals,
       [id]: !prevShownCommentModals[id],
     }));
   };

   //map 안에서 사용시 toggleCommentDelete(idx)로 사용
   ```

   문제 해결하기 위한 시도들 : history.replace('/main') 등으로 새로고침 시도(실패)

   어떻게 해결하는지 : id값을 고유값인 postId나 commentId로 사용할 것 toggleCommentDelete(postId)

   다음에는 이 문제를 발생시키지 않기 위해 어떻게 사전 작업할 것인지 : map에 들어가는 모든 것들은 영향을 받지 않는 고유값으로 줄 수 있도록 주의

## Post 컴포넌트 구성 흐름(김동우)

1. 포스트 뷰 작성하기(1개)
2. API 문서 확인하고 약속한 방식으로 data.json 만들기
3. 로컬서버와 map을 통해서 여러개의 포스트가 생성되는지, 값들이 잘 들어가는지 확인
4. 삭제화면 모달창 만들기
5. 로그인 회원가입 통신 이후 포스트 삭제 기능 구현
6. 좋아요 기능 구현
7. 댓글 달기 클릭 시 해당 댓글 input에 포커스 되는 기능 구현 (spread useState와 current.focus() 기능 사용)
8. 댓글 추가 기능 구현
9. 댓글 삭제 기능 구현
10. 댓글 삭제 기능 구현
11. 링크 공유하기 기능 구현
12. 전체적인 기능 점검
