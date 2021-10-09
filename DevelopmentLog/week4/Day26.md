# 항해 26일차

## 211008 문제해결

1. fullcalendar css:  
    그리드로 나눠도 다시 그 위에 styled 컴포넌트 적용 가능
    캘린더 css는 그 캘린더의 div 클래스이름으로 접근 가능 ex) .fc-btn  
    background-image: url("주소")
    background-cover: 커버할 방법

2. Document references must have an even number of segment; Firebase Cloud Firestore 오류 해결(https://www.youtube.com/watch?v=Tck4tN4b360)  
    처음 todo를 생성했을 때, 전체 load가 안 돼서 수정 및 삭제를 할 수 없었던 오류(수정 및 삭제는 load로 불러올 때 준 아이디로 접근하기 때문)  
    App.js에 todo의 길이를 구하는 변수를 구하고, 그걸 useEffect의 의존성 배열에 넣었다.  
    생성이 되면 todo의 길이가 변경되고, 그걸 감지해 추가된 todo까지 load를 하면서 바로 수정 및 삭제가 가능해졌다.  

3. 모달창과 이벤트 전파:  
    제일 바깥 그리드에 closeModal 함수를 걸고 선택창에서는 e.stopPropagation() 만 걸어서 closeModal의 영향을 받지 않고 바깥 부분만 클릭하면 꺼지도록 하였다.


## 일기  
오늘 인증 구현이 너무 하기 싫어 산책을 갔다왔다. 갔다오면서 다음 주에 할 아이디어가 정리되는 것 같아 나쁘지 않았다. 역시 미리 제출을 해버리면 집중이 잘 안되나보다ㅠㅠ 아마 다음주는 라이브러리를 사용해 todo+생활패턴 느낌으로 제안해보려고 한다. 멘토님이 마음에 드셨다는 팀원처럼 처음해보지만 해내겠습니다! 의 자세로 열심히 하면 다 잘 될것이라 생각한다.