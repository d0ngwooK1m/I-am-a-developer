# 항해 46일차

## 오늘 할 일

사이드 탭 로직 적고 설명하기(https://studyingych.tistory.com/60)

1. content에 필요한 컴포넌트를 담아서 TabMenu에 props로 넘겨준다

```javascript
//Settings.js
const content = [
  {
    id: "PwSettingForm",
    tab: "비밀번호 변경",
    content: <PwSettingForm />,
  },
  {
    id: "WithdrawalForm",
    tab: "회원 탈퇴",
    content: <WithdrawalForm />,
  },
];

const Settings = () => {
  return (
    <Grid>
      <p>설정 페이지</p>
      <TabMenu content={content} />
    </Grid>
  );
};

export default Settings;
```

2. useTab 함수를 통해서 버튼을 누르면 알맞은 컨텐츠가 나오는 Tab 기능을 구현한다.

```javascript
//TabMenu.js
//useTabs를 만든다. 매개변수 initialTabs는 시작할 탭 번호, allTabs는 모든 컨텐츠를 의미한다.
const useTabs = (initialTabs, allTabs) => {
  //useState hook을 통해 탭 번호 이동
  const [contentIndex, setContentIndex] = React.useState(initialTabs);

  //return값으로 tab 번호에 해당하는 컨텐츠를 contentItem으로, tab 번호를 바꿀 수 있는 useState값을 object로 리턴한다.
  return {
    contentItem: allTabs[contentIndex],
    contentChange: setContentIndex,
  };
};

const TabMenu = ({ content }) => {
  //return의 contentItem, contentChange값을 각각 배정한다.
  const { contentItem, contentChange } = useTabs(0, content);
  return (
    <Grid>
      <p>사이드 탭</p>
      <Wrapper>
        <Grid width="390px">
          {content.map((val, idx) => (
            <BtnWrapper key={val.id}>
              <Button
                _onClick={() => {
                  contentChange(idx);
                }}
              >
                {val.tab}
              </Button>
            </BtnWrapper>
          ))}
        </Grid>
        <Grid width="1050px" padding="0px 210px">
          {contentItem.content}
        </Grid>
      </Wrapper>
    </Grid>
  );
};
```

## 211028 회의

백엔드  
해쉬태그 "스트링" API 문서  
API 문서 작성 이번주까지 작성 완료

프론트엔드  
API 문서 보고 필수 기능 완성하기

디자인  
카드 수정, 회원가입, 로그인 페이지, 반응형 디자인 내용 논의

## 내일 할 일

로그인 회원가입 유효성 검사(리스폰스 적용된 다음 시작)  
유효성 검사 리프레시 토큰 적용
헤더 만들기 => 메뉴는 이모지로
