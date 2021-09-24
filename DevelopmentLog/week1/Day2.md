### 항해 2일차
오늘 한 일 : bulma로 html 및 스타일링, git main push 완료
오늘 할 일 : push 된 자료 branch 만들어서 각자 받기, bulma 설명하기, html 디자인에 대해서 이야기 하기, jinja가 무엇인지 설명하기, html 수정하기, API 작업 들어가기, 그리기 부분 꾸미기(나)

#### API
프론드엔드와 백엔드가 서로 소통하는 약속(?)을 이야기하며, 같은 url주소와 method를 가지고 있을 때 작동한다. 프론트엔드에서 필요한 자료들을 json형태로 바꾸어 전송하면, 백엔드에서 이를 받고, DB에 저장하는 등 필요한 처리를 하고, 그 결과를 다시 프론트엔드에 알린다.  
이번 프로젝트에서는 기능별로 맡아 서로 헷갈리지 않고 할 수 있었지만, 심화 과정에는 API 작성시 프론트엔드와 백엔드의 의사소통이 더욱 중요해질 것 같다!  
+) 그림 데이터를 DB에 저장했는데 양이 엄청나다 뷰로 뿌려지는지 확인하고 안되면 강의목록에 있는 파일 업로드 기능을 써야하나 고민중이다.

#### Canvas
html 태그이며, 말 그대로 캔버스를 그릴 수 있고, 자바스크립트로 이를 이용해 여러가지 움직임과 관련된 효과들을 낼 수 있다. 이를 활용하여 그림 그리기 기능을 넣어보았다. 사용자가 직접 그릴 수 있는 기능을 만드는 것이 아주 재미있었다.

#### 임민영 튜터님 REACT 강연
튜터님 관점: 사용성이 편한게 최고!
더 재밌는 분야를 해라!
기술이나 트렌드는 중요한게 아니다! 지금 주어진 걸 열심히 배우고 문제를 해결하는 능력을 기르는 일이 더 중요하다!
오류를 두려워하지 마라 취업하기전에 최대한 오류를 경험하고, 해결하면 내 성장에 엄청난 도움을 준다!
페이스북 개발자 그룹 => 개발 아티클 올리는 사람들이 많다 => 신기술 동향 파악 => 입맛에 맞는 기술 공부
바닐라 자바스크립트는 어려울 수 밖에 없다. => 맨땅에 헤딩하는 느낌
코드는 많이 쓸수록 는다!!(김성근 감독님 느낌) 이해가 안되면 될 때까지 써본다!!

#### 일기
캔버스 기능을 하면서 프론트엔드는 이런 일을 하는구나 라는 생각을 하게 되었다. 아주 재밌었고, 개인적으로 더 이런 캔버스를 활용한 인터랙티브 한 것들을 많이 만들어 보고 싶다는 생각이 들었다.  
내 공부 방식이 맨땅에 헤딩하는 느낌이어서 이게 맞나 하는 생각이 들었는데, 오늘 튜터님이 많이 깨질수록 나중에 성장을 더 빠르게 한다는 이야기를 듣고 잘 하고 있구나 라는 생각이 들었다. 앞으로 더 헤딩해봐야겠다! 어쩌면 맨땅이 깨질지도 모르는 일이다ㅋㅋㅋ  
오늘은 로그인 기능에서 문제가 발생했다. 내가 담당했던 부분이라서 자신감이 넘쳤는데 이게 웬걸, 자리를 파할 때 까지 전혀 해결하지 못했다... 이 일기를 업로드 하고 다시 조원들과 다시 봐야겠다! 내일까지는 풀리기를 바라며...🙏  
+)12시 지나기 전에 극적으로 해결이 되었다! 문제는 js에서 cookie 저장을 할 때 
```javascript
$.cookie("login_token", response["login_token"], { path: "/" });
```
요기서 path를 지정해주지 않았던 것이 원인이었다... 이 차이를 알아채서 일찍 잘 수 있게 해준 승준님에게 박수를 보낸다 👍