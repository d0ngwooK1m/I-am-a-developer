### 항해 5일차
오늘 할 일
1.CSS 정리(아영님): 
* 회원가입 프로필 사진 중앙에 오도록 하기
* 포스팅 카드리스트 사진과 글 사이 선으로 구분하기
* 카드리스트 쌓일 때 차곡차곡 쌓이도록 하기
* 그 외에 디자인 적으로 놓친 부분이 있다면 같이 최종점검하고 수정하기  

2.배포 전 기능 확인(대수님, 나):
* 기능적인 부분 체크하고 오류없는지 확인(우선적으로 API문서에 있는 기능은 이상없이 있는지 확인)  
ex) 게스트 포스팅 접근금지 설정, 게스트 메인페이지 하트 클릭 시 접근금지 설정, 비밀번호 찾기 기능이 없으므로 비밀번호 정규식은 주석처리하기 등 
valueOf().innerText로 환영문구 감지해서 포스팅 접근금지 설정 =>회원가입 js에서 guest 닉네임으로 못쓰게 처리 필요
* 웹사이트 구동에 영향을 주지 않는 오류(두번 클릭하면 두번 저장된다던지), 기능적으로 아쉬운 부분 체크 후 노션에 메모
* API 문서, 와이어 프레임 그림 현재 기능에 맞게 수정  

3.대망의 배포(승준님):  
* 원격서버 구현 및 DB연결 코드 로컬에서 서버로 걸어주기
* 현재 1차 목표는 nohup 연결하기 전으로 완료(나중에 추가 작업이 있어도 원활한 파일 업데이트가 이루어질 수 있도록)
서버이슈 발생: token = jwt.encode(payload, SECRET_KEY, algorithm='HS256').decode('utf-8') 로컬에선 decode 없어야 작동, 서버에선 있어야 작동. => (추측)window와 ubuntu가 datetime을 불러오는 방식이 달라서 생기는 문제인 듯 하다.

4.최종수정(다같이) 및 최종 업로드:
* 2.배포전 기능확인 에서 인지했던 오류, 기능상 문제 보완
* 시간 체크 후, 시간이 많이 남았다면 추가 기능 할지 논의 후 적용
* 최종 파일 서버에 업로드 후 nohup 걸어주기

5.최종 배포 완료 후(다같이):
* 데모영상 찍기
* 데모영상 썸네일 이미지 만들기
* 깃허브 최종정리
* 끝!✌😎

내일 할 일: 카드 이모티콘 위치 마이, 메인페이지 통일하기, 회원가입 인풋 플레이스 홀더에 비밀번호 작성법 삭제, 프로필 사진 중앙으로(아영님이 작성완료), 게스트일때 퀴즈 접근제한

#### 일기
최종제출 완료! 매니저님이 계속 머물고 싶은 서비스라고 해주셨다! 이보다 더한 칭찬이 있을까? 조원들과 이 기쁨을 계속 나누고 싶다ㅎㅎ 오늘은 꿀잠잘 수 있겠다!!!!
