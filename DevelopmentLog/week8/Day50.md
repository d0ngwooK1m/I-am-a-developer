# 항해 50일차

## 오늘 할 일

- 로그인

1.  email: 'testkiim@gmail.com', pw: 'qwerqwer1' OK
    errorMessage: '회원 정보를 찾을 수 없습니다.'
2.  email: 'testkim@gmail.com', pw: 'qwerqwer111' OK
    errorMessage: '비밀번호가 일치하지 않습니다.'

- 회원가입

1. email: 'testkim2@gmail.com', pw: 'qwerqwer55', pwCheck: 'qwerqwer1', userName: '김테스트2' OK
   errorMessage: '비밀번호가 일치하지 않습니다.'

2. email: 'testkim@@gmail.com', pw: 'qwerqwre1', pwCheck: 'qwreqwer1', userName: '테스트킴' OK
   errorMessage: '이메일 형식이 올바르지 않습니다.'

3. email: 'testkim5@gmail.com', pw: '', pwCheck: 'qwerqwre1', userName: '킴테스트' CHECK OK?
   errorMessage: '회원정보를 입력해주세요.'  
   =>비밀번호 입력해주세요는 어디서 나오는 에러인지 물어볼 것 => 빈값일 때 회원정보를 입력해주세요로 통일

4. email: 'testkim4@gmail.com', pw: 'qwerqwerqqqqqqqqqqqqqqqqqqqqqqqqqqq', pwCheck: "qwerqwerqqqqqqqqqqqqqqqqqqqqqqqqqqq'", userName: '테스트킴4' OK
   errorMessage: '비밀번호는 6~20자리로 해주세요'

- 이메일 중복체크

1. email: 'testkim@gmail.com' OK?  
   message: '중복된 email이 존재합니다.' => errorMessage로 통일 필요

- 닉네임 중복체크

1. userName: '김테스트' OK?
   message: '중복된 닉네임이 있습니다.' => errorMessage로 통일 필요

- 비밀번호 변경

1. 비밀번호 변경 OK

2. qwerqwer2 qwerqwer2 qwerqwer2 FAIL => OK
   errorMessage: "새로운 비밀번호와 비밀번호확인이 같지 않습니다" => 변경비밀번호와 현재 비밀번호가 같습니다 로 바뀌어야 할 듯 => 변경완료

3. qwerqwer2 qwerqwer3 qwerqwer2 OK
   errorMessage: '새로운 비밀번호와 비밀번호확인이 같지 않습니다'

4. qwerqwer1 공란 공란 OK
   errorMessage: '변경할 비밀번호를 입력해주세요'

5. 공란 qwerqwer2 qwerqwer2 OK  
   errorMessage: '현재비밀번호를 입력해주세요.'

- 회원탈퇴
  비밀번호 틀리기 ?
  회원탈퇴 성공

==> DELETE에 Body data?

## 211101 회의

### 백엔드 공유사항

혜림님: formdata 문제점 해결 => 파일값은 들어오나 프론트에서 null로 들어오는 값 때문에 문제가 발생하는 듯 확인 필요...
승준님: 레디스 공부중...
준석님: 소켓 공부중...

### 프론트엔드 공유사항

동우: 오류체크, 유효성 검사 벨로퍼트 자료 참조해서 시작...
아영님: 마이페이지 프로필 수정페이지 뷰 바꾸기, 프로젝트 추가하기 진행...
우석님: 컨탭페이지 모달컴포넌트 새로 생성 및 작업...

### 디자인 공유사항

민지님: 와이어 프레임 완성 및 세부사항 공유, 수정

url 확인
