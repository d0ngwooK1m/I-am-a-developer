# 항해 80일차

## 0. 소개

안녕하십니까 발표를 맡게 된 16조 팀장 김동우입니다. 프로젝트 Contap 발표 시작하도록 하겠습니다.

## 1. 우리가 해결하려는 문제

백엔드와 프론트엔드의 프로젝트나 협업은 생각보다 쉽지 않습니다. 디자이너와의 협업은 더더욱 쉽지 않구요.
그러기 힘든 이유는 서로를 알 수 있는 정보들이 한 곳에 모여있지 않아서, 그 정보를 보고 이야기를 할 수 있는 공간이 많지 않아서라고 생각했습니다.
그래서 저희는 이 문제를 해결하고자 개발자와 디자이너가 서로의 프로젝트를 공유하고 채팅으로 이야기 할 수 있는 사이트인 Contap을 만들게 되었습니다. 시연 영상 보시겠습니다.

## 2. 시연영상

저는 처음 가입을 한 상태입니다. 튜토리얼을 따라 마이페이지로 들어가 앞면 카드에 들어갈 제 분야와 프로필 사진을 선택합니다. 그리고 제 스택을 검색해 넣습니다. 그리고 본인이 프로젝트를 할때 가지는 관심사 또한 세가지 골라서 넣습니다. 그 다음 자신의 프로젝트를 소개하는 뒷면카드를 작성합니다. 제목, 내용 프로젝트 링크 등을 넣을 수 있습니다. 그리고 다음 튜토리얼에 해당하는 알람 설정을 합니다. 알람을 켜고 본인의 전화번호를 저장하면 로그인 상태가 아닐 때 알람으로 친구신청이 됐는지 알려줍니다. 튜토리얼이 끝났다면 원하는 카드를 탐색할 수 있습니다. 그리고 프로젝트 링크를 확인하여 같이 프로젝트를 하고 싶다면 메세지와 함께 친구 신청 기능인 탭 신청을 할 수 있습니다. 상대방이 탭을 받아준다면 나의 그랩에서 확인할 수 있으며, 메세지를 보내 자유롭게 프로젝트에 대한 이야기를 나눌 수 있습니다.

## 3. 핵심기능

## 3-1. 카드탐색

첫번째는 카드 탐색 기능입니다. 로그인 시 마이페이지에서 본인의 프로젝트 카드를 작성하게 됩니다. 그 후 다른 사람이 작성한 카드 뒷면을 탐색하고, 프로젝트 자세히 보기 버튼을 통해 자세한 설명을 확인할 수 있게끔 하였습니다. 그 정보를 통해서 다른 사람에게 채팅을 신청(탭) 할 수 있도록 하는 중요한 기능이라고 할 수 있겠습니다.

## 3-2. 알람기능

다음은 문자 알람 기능입니다. 현재 실시간알람 기능이 존재하지만 실질적으로 웹사이트를 접속하지 않은상태에선 확인이 불가능하기 때문에 탭요청이 왔을때 웹사이트에 접속하지 않았더라도 본인의 휴대폰등록을 통해 문자로 알람이 전송되게끔 구성했습니다.

## 3-3. 채팅기능

저희 조는 채팅기능에 기본적으로 알람, 최신순으로 채팅방을 정렬, 안 읽은 메시지가 있음을 알리는 기능들 있어야한다고 생각했습니다. 위의 기능은 새 메시지가 발생할때마다 데이터를 저장해줘야지만 가능한 기능입니다, 하지만 저희조는 1초에도 수십개 또는 수백개의 메시지가 발생할수있는 서비스를 고려해봤을때 새 메시지가 발생할때마다 데이터 베이스에 값을 insert하거나 update하는 방식은 좋지 못하다고 판단하였고 위 기능에 필요한 정보들을 redis 에 저장하는 방식으로 구현했습니다. 영상에서 보시는 것과 같이 최신순으로 메세지가 정렬된 모습을 보실 수 있습니다.

## 4. 기술 스택

다음으로는 저희가 개발에 사용한 기술스택을 설명드리겠습니다.  
기술스택으로 프론트엔드는 언어로 Javascript, 라이브러리로는 React, Redux, Websocket, axios, styled-component 등을 사용하였고, 백엔드는 언어로 Java, 프레임워크 및 라이브러리로는 Spring Boot, Websocket, queryDSL, Swagger, sentry 등을 사용하였습니다.
(센트리 이미지 추가)

## 5. 아키텍쳐 구조

다음은 아키텍쳐 구조입니다.  
우선 왼쪽 프론트엔드는 yarn으로 빌드파일을 생성합니다. 그리고 S3로 배포를, CloudFront로 https 처리과정을 거칩니다. 그리고 Route 53으로 도메인 처리를 합니다.  
오른쪽 백엔드는 Github Action에서 프로젝트 빌드 후, jar 파일을 zip파일로 압축해서 S3에 업로드하고 CodeDeploy는 S3에서 파일을 받아 EC2에 배포를 진행합니다. 채팅 기능을 사용할 땐 Redis를, CRUD 기능을 사용할 땐 MySQL를 사용합니다. 또한 이미지 저장 기능을 사용할 땐 S3를 사용합니다. 최종적으로 백엔드와 프론트엔드가 각각 ssl 인증서를 받아서 https를 적용해 통신합니다.

<!-- (백엔드 수정) Github Action에서 프로젝트 빌드 후, jar 파일을 zip파일로 압축해서 S3에 업로드하고 CodeDeploy(정확히는 CodeDeploy Agent이지만, 그냥 CodeDeploy라고 하셔도 될 것 같습니다.)는 S3에서 파일을 받아 EC2에 배포를 진행합니다. -->

## 5.5 아키텍쳐와 관련된 기술 설명

아키텍쳐 구조에서 사용했던 중요한 기술들을 자세히 설명해보겠습니다.
우선 Redis는 pub/sub 기능과 key/value 기능을 사용하기 위해 redis를 사용하였습니다.
QueryDSL은 데이터 베이스를 조회하기 위해 사용했습니다.
S3-EC2는 사진 저장 시 AmazonS3 SDK메소드(putObject,deleteObject)를 이용해 추가/삭제 관리를 편리하게 하고 로컬메모리를 아낄 수 있기 때문에 사용했습니다. 또한 프론트엔드에서 관리 시, 사용자가 데이터를 수정할 수 있는 위험을 방지할 수 있어 백엔드에서 관리하도록 사용했습니다.
Github Action은 자동배포를 통해 자주 여러번 수정배포하면서 개발의 효율성을 높이고 릴리즈기간도 단축할수 있는 장점이 있고, 이를 선택한 이유는 Github와 통합되어 있어 별다른 복잡한 절차 없이 Github를 통해 사용할 수 있어 선택했습니다.
SSL은 백엔트 프론트엔드 둘다 ssl인증서를 발급받아 최종적으로는 http 보다 보안성이 강화된 https를 사용하였습니다.

## 6. 프론트엔드 문제해결

프론트엔드에서 생각한 기술적 도전(및 문제해결)입니다.

## 6-1. 알람 기능

프로젝트를 같이 하기 위해 필요한 사람을 구하는 것이 핵심 목표인 만큼 실시간으로 알림을 주고 받는 것에 집중 했습니다.
유저가 로그인을 하는 순간 노티룸에 소켓으로 연결이 됩니다. 그러므로 현재 사이트에 로그인 한 모든 유저는 노티룸에 들어갑니다.
그 후 채팅 창을 열게 되면 챗룸에 연결 되는데 챗룸에서 채팅을 보내면 상대방이 같은 챗룸에 들어와 있는지 체크를 하게 됩니다. 만약 채팅방에 상대방이 들어와 있지 않다면 노티룸에서 그 유저를 찾아 알람 메시지를 보냅니다. 그럼 그 메시지를 가지고 상대방에게 알람 아이콘을 띄워주도록 로직을 구성 했습니다.
탭을 보내고 받을 때 역시 노티룸에서 해당하는 유저를 찾아 알람 메시지를 보내고 아이콘을 띄워 줍니다.
[스페이스바]
알람을 받아야 하는 유저가 사이트에 들어와 있지 않아 노티룸에서 찾을 수 없다면 타겟 유저가 로그인 할 떄 받는 리스폰스에 알람 내역을 같이 받아서 해당하는 알람에 따라 아이콘을 보여줍니다. 해당 타겟 유저가 핸드폰 번호를 등록 한 상태라면 탭 요청을 받았을 때는 문자로 알람을 받을 수 있도록 하였습니다.
[스페이스바]
Login 버튼을 누를 시 노티룸에 연결 되도록 하기 위해 root페이지에서 유즈이펙트로 소켓에 연결 했었는데 유저가 다른 페이지에서 새로고침을 할 시 소켓에 연결을 할 수 없는 이슈가 있었습니다. 해당 이슈를 해결하기 위해서 모든 페이지에서 연결하기 위해 헤더 컴포넌트에서 소켓에 연결 하도록 변경 했었으나 기능적인 분리가 안 돼있다는 생각이 들어서 소켓을 연결하는 컴포넌트를 따로 만들어서 App.js에서 모든 컴포넌트에 적용 될 수 있도록 변경 하였습니다.

## 6-2. 튜토리얼

처음 사이트를 이용하는 유저들을 위해 마이페이지 튜토리얼, 알람 설정 튜토리얼을 적용하여 카드를 만들고, 알람 설정을 할 수 있도록 유도하였습니다.
로그인 유저에게 백엔드가 로그인 및 새로고침 시 알람 정보를 제공하며, 여기에 튜토리얼들을 읽었는지 여부도 포함되어 있습니다.
이 값을 리덕스에 저장하여 튜토리얼을 읽지 않은 유저에게 react-joyride로 만든 마이페이지 튜토리얼을 먼저 제공하고, 유저가 창을 닫거나 마이페이지 버튼을 클릭했을 때 튜토리얼이 닫히고, 유저가 튜토리얼을 읽었다는 API를 전송합니다. 마이페이지 카드 작성이 끝난 다음 메인페이지로 돌아가면 조건문에 의해 알람설정 튜토리얼이 뜨게되고, 모든 튜토리얼을 확인한 다음부터는 로그인 할 때마다 튜토리얼 읽음으로 처리해 더 이상 뜨지 않도록 하였습니다.

## 7. 백엔드 문제해결

백엔드에서 생각한 기술적 도전(및 문제해결)입니다.

## 7-1. boolean 자료형 저장방식

저희조는 계속되는 요청에 DB에 단순한 Boolean형태 데이터가(알람설정과 같은 정보) 컬럼으로 추가됨으로써 , 칼럼을 많이 생성하는 것은 비효율적이라 생각되었습니다.
그래서 비트연산을 사용하면 여러가지 Boolean 데이터를 한 칼럼안에 저장 할 수 있기 때문에 최대 32개 데이터를 하나의 int형으로 저장하는 방식으로 구현하였습니다.

## 7-2. 검색 기능

(기존테이블 이미지를 보여주면서)
저희 서비스의 User와 HasTag의 테이블구조는 보이는 이미지와 같은 형태로 구성되어 있는데요 , HashTag로 검색을하면 선택한 HashTag를 토대로 User가 검색결과로 도출 되게끔 구현하려 했습니다. 여기서 User 테이블과 HashTag테이블이 다대다 관계를 갖고있기에 중간테이블이 존재했는데, 기존에는 JPQL을 사용하고 있어 and검색을 하기엔 쿼리문이 너무 복잡해져 OR검색으로 구현하였습니다,여기서 and검색을 구현하기 위해선 어떻게 해야할지 고민 하던중 User와 HashTag의 관계를 중간테이블에서 관리하는것이 아닌 User테이블에서 HashTag에 관련된 데이터를 관리하면 어떨까 라는 생각을 했었는데 이러한 방식이 반정규화라는 것임을 알게되었습니다.

(반정규화된 테이블 이미지를 보여주면서)
User테이블에 HashTagString이라는 String 자료형 컬럼을 추가하고 축구와 Java를 좋아하는 유저라면 (@Java@\_@축구@ 가리키며) 다음과 같은 형태로 저장하였습니다.
이렇게 함으로서 이전에 포기했던 and검색을 구현할 수 있게 되었고,성능적인 면에서도 테스트를 진행 하였는데 5000명의 User가 랜덤한 HasTag 4개를 갖도록 설정해준 뒤에 중간테이블을 사용한 검색과 반정규화한 테이블을 사용한 검색을 비교하였을때 전자는 11.6ms가 나왔고 후자는 7.63ms가 나왔기 때문에 최종적으로는 반정규화한 테이블을 사용한 검색을 적용하였습니다.

## 8. 고객반응 및 개선점

항해 크루원들을 대상으로 클라이언트 피드백을 받았었는데 카드 작성시 뭘 해야할지 모르겠다는 피드백이 정말 많았습니다.
가장 핵심이 되야 할 기능이 직관적이지 못하다는 점은 저희한테 너무 큰 약점이 될 것 같아 어떻게든 해결을 해야한다는 결론이 나왔습니다.
[스페이스바]
이처럼 튜토리얼을 만들어 유저들이 카드를 작성할 수 있도록 유도하였습니다.
우선 기본적으로 카드 형식으로 프로젝트를 보여주기 때문에 제약이 많았었고.
기획 단계부터 Closed Community형식으로 가기위해 뒷면카드를 작성하지 않으면 다른사람의 카드를 열람하지 못하게 했었으나 그렇게 하니 오히려 카드 작성이 힘든 결과를 만든 것 같아 두가지 해결 방법을 생각했었습니다.
첫번째는 Closed Community를 유지하고 온보딩 형식으로 카드작성 가이드를 보여준다. 였고
두번째는 뒷면 카드 열람권한을 로그인만 하면 가능하게 하여 사용자가 직접 카드를 탐색하여 작성할 수 있게 한다. 였는데
전자의 방법은 너무 강제성이 강할 것 같고 아무래도 하나하나 설명하는 사이트가 좋은 사이트 처럼 보이지는 않아서
[스페이스바]
아래 사진 처럼 PlaceHolder로 최대한 상세하게 알려주는 것을 전제로 후자를 택하게 되었습니다.
다음으로는 백엔드, 프론트엔드의 카드 색도 구분이 되었으면 좋겠다는 피드백이 많이 있었습니다.
핵심 기능은 개발자와 디자이너의 매칭이기 때문에 개발자 끼리의 색 구분은 크게 의미가 없다고 생각 했었으나 생각보다 많은 피드백이 와서 많은 고민을 했습니다.
[스페이스바]
색을 추가하는 간단한 작업 이지만 이 또한 사이트의 메인 컬러라고 할 수 있기 때문에 정말 신중하게 색을 고르고 아래와 같이 적용하게 되었습니다.

## 9. 지금까지 성과와 앞으로 계획

저희 서비스를 이용한 총 유저수는 71명, 카드를 하나라도 작성한 유저는 46명이 나왔습니다.
회원가입만 하고 카드를 둘러보고 나간 인원이 적지 않다고 판단되어 카드를 작성했을 때만 뒷면을 볼 수 있도록 하는 방향으로 보완할 계획입니다.

설문조사 참여 인원은 20명입니다.
설문조사에서 공통적인 피드백으로 검색이 불편하다, 스택이 복수선택 되면 좋겠다, 커뮤니티 게시판이 있었으면 좋겠다 같은 피드백이 주로 나왔습니다.
그 외에 디자인이 좋다, 카드 형식이 마음에 든다, 채팅기능이 잘 된다 같은 좋은 피드백도 있었습니다.
조사에서 나온 피드백은 꾸준히 수정 보완하여 더 멋진 컨탭을 만들도록 할 예정입니다!

<!-- 7. 최종 성과 및 지표입니다. -->