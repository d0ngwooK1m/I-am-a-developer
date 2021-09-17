### 항해 4일차
오늘 할 일:  
0.닉네임 수정한 부분 공유하고 push 및 merge  

1.디자인 사이트 보고 CSS 컨셉 정하기  
* https://thefwa.com/
* https://www.awwwards.com/
* https://www.behance.net/

2.디테일한 부분 파트 분배하여 작업완료하기: 
* 이미지 선택하지 않을 시 기본 이미지가 설정되도록 하기
* 이메일 및 닉네임 중복확인(닉네임 쪽은 옵션)
* 정규표현식을 이용한 이메일 양식제한 
* 이메일, 비밀번호 및 비밀번호 확인 input type 바꾸기
* ~~로그인, 회원가입 페이지 실패 시 오류 나타나게 하기~~
* 일기 작성 시 날짜처리 어떻게 할 것인지, 날씨를 오늘 기분 표현하기로 바꿀 것인지 등...

3.컴포넌트 파트분배 맡아서 컨셉에 맞게 디자인 사용하기  

4.최종추가 기능 결정, 파트분배 및 와이어 프레임 API 수정, 디자인컨셉 맞추기
* 최상단 버튼(빨리 끝나면 기분에 따라 로그인 시 모달창으로 메세지 주기 기능?)
* 그리기 부분 추가 작업(화면 배경색, 펜이나 지우개 크기 조절, 색 여러개 넣기)
* 좋아요 기능 생성
* 날짜에 맞는 등수 정하기(1주일 간격으로)  
내일 점심까지 진행하면 될 것 같다.

궁금한 사항: 
* 날짜 기능을 넣게 되면 그리기 페이지의 날짜 기능은 없애야 하는게 아닌가?
* 일기인데 하루에 하나만 작성 가능하게 해야하는 것이 아닌가?

#### 정규표현식
정규표현식은 봐도봐도 어렵다... 오늘 확실히 안 정보는 시작과 끝은 /^ $/ 이렇게 된다는 것이다. 오늘 즐겨찾기한 사이트들 자꾸 참조하다보면 더 적응되지 않을까? 생각한다. 글자수 제한은 {최소 수, 최대 수} 이런식으로 하는데 최소 수만 정하려면 {최소 수} 이렇게만 작성하면 되는 것 같다. 나중에 다시 확인해보자! (닉네임과 비밀번호 정규표현식으로 제한)

#### 캔버스
그림 굵기 바꾸기, 화면 압축했을 때 좌표계산하기를 했다. 좌표계산하기 부분은 나중에 천천히 다시 한번 봐야겠다.

#### 날짜 바꿔주기
멍청한 실수를 헀다. 승준님이 말해준 덕분에 해결할 수 있었다 흑흑
```javascript
submitBtn.addEventListener('click', () => {
    const today = new Date();
    const year = today.getFullYear();
    let month = today.getMonth();
    if (month < 10) {
        month = `0${today.getMonth()+1}`;
    }
    let date = today.getDate();
    if (date < 10) {
        date = `0${today.getDate()}`
    }

    // let date_give = document.querySelector('.diary-date');
    let date_give = document.getElementById('date-box').value;
    console.log(date_give)
    if (date_give == "") {
        date_give = `${year}-${month}-${date}`;
    }
    console.log(date_give)
    const url = canvas.toDataURL('image/png');
    //🔥
    let weather = weather_give.options[weather_give.selectedIndex].value;
    if(weather == '날씨')
        weather = '☹'
    const postData = {
        img: url,
        date: date_give,
        weather: weather,
        comment: comment_give.value,
    }

    fetch('/mainpage/post', {
        method: "POST",
        headers: {
            "Content-Type": "application/json",
        },
        body: JSON.stringify(postData),
    })
        .then((response) => response.json())
        .then((response) => {
            // console.log(response);
            alert(response["result"]);
            window.location.href = '/';
        })
});
```
여기서 date_give를 addEventListener 밖에서  주니 크롬은 '로딩할 때 읽어달란 거군 ㅇㅋ' 하면서 최초상태인 ""를 읽어오는 것이다. 앞으로 이런 실수를 하지 않도록 주의해야겠다! 그래도 부딪혀서 해결하니 속은 시원하다ㅋㅋㅋ

#### 일기
예상했던 만큼 작업을 하고 모든 기능을 추가하진 못했지만 몇가지를 더 추가할 수 있었다. 이때까지 날 이끌어주고, 또 잘 따라와준 팀원들에게 감사하다😭 내일부터는 약간의 CSS 정리가 끝나면 바로 배포를 시작할 예정이다.