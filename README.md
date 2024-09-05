# 이주형 202030324
# 9월 4일 강의
<프로젝트 생성 방법>

- 만일 개발환경에 yarn 패키지가 설치되어 있다면 Next.js는 yarn을 사용하여 프로젝트를 초기화 합니다.

- (yarn이 설치되어 있을 때) npm을 기본으로 사용하고 싶다면 다음 명령으로 설정을 덮어쓸 수 있습니다.

        npx create-next-app <app-name> --use-npm

- 또 다른 프로젝트 생성 방법으로는 GitHub 저장소에서 원하는 보일러플레이트 코드를 다운로드해서 새 Next.js 프로젝트를 시작할 수도 있습니다.

        npx create-next-app --example<보일어플레이트 이름>
        
            npx create-next-app --example blog-starter
<프로젝트의 기본 구조>

- Next.js는 네비게이션을 구현할 때 react-router와 같은 라이브러리를 사용하지 않고, pages/디렉토리를 사용합니다.

- Next13.4 후반부터 pages가 app으로 변경되었습니다. 교재에 나와 있는 pages는 모두 app으로 변경하여 사용하면 됩니다.

- 현재 Next 14.2.5이며, 15도 pre-release되었고 곧 정식 출시될 예정이다.

    https://github.com/vercel/next.js/releases

- pages/디렉토리 안의 모든 js파일은 public 페이지가 됩니다.

- pages/의 index.js파일을 복사해서, about.js로 이름을 바꾸면, http://localhost:3000/about 으로 접속 할 수 있습니다.

    -> 확인을 위해 about.js 페이지를 조금 수정해 주세요.
    
    -> 라우팅과 관련해서는 뒤에서 다시 살펴 보기로 합니다.

- public/ 디렉토리에는 웹 사이트의 모든 퍼블릭 페이지와 정적 콘텐츠가 있습니다.

    -> 이미지, 컴파일된 css, 컴파일된 js, 폰트 등.

- styles/ 디렉토리에는 앱에서 사용하는 스타일시트 넣습니다.

    -> 하지만 이 디렉토리가 반드시 필요한 것은 아닙니다.

- 