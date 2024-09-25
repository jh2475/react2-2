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
- 용도가 정해져 있는 디렉토리는 pages/와 public/ 뿐입니다.
- 나머지 디렉토리는 필요에 따라서 다른 목적으로 사용하거나 삭제해도 됩니다.

    -> 프로젝트 root에 필요한 디렉토리를 새로 생성해서 사용해도 됩니다.

<타입스크립트 지원>
- Next.js는 타입스크립트로 작성되었기 때문에 고품질의 type definition을 지원합니다.
- 기본 언어를 타입스크립트로 지정하려면 root에 tsconfig.json이라는 설정파일 생성하면 됩니다.
- 그런 다음 npm run dev 명령을 실행하면 다음과 같은 메시지를 확인할 수 있습니다.

    -> 이 메시지는 주 언어에 대한 의존성 패키지를 설치해 달라는 내용입니다.

    -> 패키지를 설치하고 나면 비어 있던 tsconfig.json 파일의 내용이 자동으로 채워집니다.

    -> vscode를 사용하면 설정 내용이 자동으로 채워지기 때문에 별도의 설치는 필요하지 않습니다.

        It looks like you're trying to use TypeScript but do not have the required package(s) installed.

        Please install typescript, @types/react, and @types/node by running;

            npm install --save-dev typescript @types/react @types/node

        If you are not trying to use TypeScript, please remove the tsconfig.json file from your package root (and any TypeScript files in your pages directory).
<바벨과 웹팩 설정 커스터마이징>
- 바벨이나 웹팩의 설정도 커스터마이징 할 수 있습니다.

- 바벨은 자바스크립트 트랜스컴파일러이며, 최신 자바스크립트 코드를 하위 호환성을 보장하는 스크립트 코드로 변환하는 일을 담당합니다.
- 하위 호환성이 보장되면 어떤 웹 브라우저에서든 자바스크립트 코드를 실행할 수 있습니다.
- 바벨을 사용하면 브라우저나 Node.js 등에서 지원하지 않는 새롭고 훌륭한 기능을 현재의 환경에서도 실행할 수 있습니다.
- 바벨 설정을 커스터마이징 하려면, 프로젝트 Root에 .babelrc 라는 파일을 생성하면 됩니다.
- 이 설정 파일을 비워 두면 오류가 발생하기 때문에 최소한 다음 내용을 저장해야 합니다.

        {
            "presets": ["next/babel"]
        }
# 9월 11일 강의
<ECMAScript 기능 중 파이프라인 연산자를 사용해 보자.>
- 파이프라인은 공식적으로 채택되지 않은 연산자 입니다.
        
        console.log(Math.random() * 10);
        // 파이프라인 연산자를 사용하면 위 코드를 아래와 같이 바꿀 수 있습니다.
        Math.random()
            |> x => x * 10
            |> console.log;
- 기능을 사용하려면 바벨 플러그인을 설치해야 합니다.

        npm install --save-dev @babel/plugin-proposal-pipeline-operator @babel/core
- 그리고 .babelrc 파일을 다음과 같이 수정합니다.

        {
            "presets": ["next/babel"],
            "plugins": [
                [
                    "@babel/plugin-proposal-pipeline-operator",
                    { "proposal": "fsharp" }
                ]
            ]
        }
- 이제 개발 서버를 재 시작하면 됩니다.

<그 밖에 설정...>
- 개발 시 타입스크립트를 주 언어로 쓰고 싶다면 앞서 살펴본 것과 같은 방법으로 타입스크립트 전용 플러그인을 설치하고 설정을 바꿔 주면 됩니다.
- 프로젝트를 생성할 때 선택할 수 있기 때문에 생성할 때 설정할 것을 추천합니다.

- 웹팩은 특정 라이브러리, 페이지, 기능에 대해 컴파일된 코드를 전부 포함하는 번들을 만들어 줍니다.
- 라이브러리와 여러 개의 컴포넌트로 구성된 페이지를 개발했다면, 웹팩은 이 것을 하나의 번들로 합쳐줍니다.
- 만일 SASS나 LESS 같은 CSS 전처리기를 사용해서 개발하고 싶다면, 웹팩 설정을 수정해 주면 됩니다. (설정 방법은 취급하지 않습니다.)

<몇가지 일어날 수 있는 오류>
- 처음 Next 프로젝트를 생성할 때 오류로 생성되지 않는 경우가 있습니다. 이 것은 CRA가 설치되어 있지 않아서 생기는 현상입니다. 이런 경우는 다음과 같이 create-react-app을 Global로 설치해 주면 됩니다.

$ npm i -g create-react-app

이제 프로젝트를 생성합니다.

$ npx create-next-app@latest

- Next.js 12 이후 babel을 지원이 중지 되었습니다. 이제 SWC로 그 기능이 대체 되었습니다. 따라서 최신 환경에서 babel설정을 하게 되면 오류가 발생합니다. 당연히 babel을 제거하면 오류는 사라집니다.
- 만일 SWC를 사용하고 싶다면 다음과 같이 12 혹은 최신 버전의 Next프로젝트를 생성해 주면 자동으로 설정됩니다.

$ npx create-next-app@12 or npx create-next-app@latest

<렌더링 전략>
- 렌더링 전략이란 웹 페이지 또는 웹 애플리케이션을 웹 브라우저에 제공하는 방법을 의미합니다.

- 정적인 페이지 제작에는 Gatsby를 추천합니다.

- 서버 사이드 렌더링 전략을 원한다면 다른 프레임워크를 검토해 보세요.

- 그런데 Next.js에서는 이 모든 방법을 완전히 새로운 수준으로 제공합니다.

- 어떤 페이지는 빌드 시점에 정적으로 생성하고, 어떤 페이지는 실행 시점에 동적으로 생성할지 쉽게 정할 수 있습니다.

- 또한 특정 페이지에 대한 요청이 있을 때마다 페이지를 다시 생성할 수도 있습니다.

- 그리고 반드시 클라이언트에서 렌더링해야 할 컴포넌트도 지정할 수 있어서 개발이 쉽습니다.

<서버 사이드 렌더링(SSR)>

- 생소할 수도 있지만 웹 페이지를 제공하는 가장 흔한 방법입니다.

- APM을 이용하는 일반적인 웹 페이지 생성이라고 보면 됩니다.

- 여기에 자바스크립트 코드가 적재되면 동적으로 페이지 내용을 렌더링합니다.

- Next.js도 이와 같이 동적으로 페이지를 렌더링할 수 있습니다.

- 그리고 여기에 스크립트 코드를 집어 넣어서 나중에 웹 페이지를 동적으로 처리할 수도 있는데 이를 하이드레이션이라고 합니다.

- 예를 들면 어떤 사람이 작성한 블로그 글을 한 페이지에 모아서 작성해야 한다면 SSR을 이용하는 것이 적당합니다.

- 서버 사이드 렌더링 -> 자바스크립트가 화이드레이션된 페이지를 전송 -> 클라이언트에서 DOM 위에 각 스크립트 코드를 하이드레이션 : 페이지 새로 고침 없이 사용자와 웹 페이지간 상호 작용을 가능하게 합니다.
# 9월 25일 강의
<Next.js 공식문서의 Data Fetching 예제>

- https://nextjs.org/docs/app/building-your-application/data-fetching/fetching

        export default async function Page() {
            let data = await fetch('https://api.vercel.app/blog')
            let posts = await data.json()
            return (
                <ul>
                    {posts.map((post) => (
                        <li key={post.id}>{post.title}</li>
                    ))}
                </ul>
            )
        }
- 
        코드
- Page Router에서는 SSR을 위해서 getServerSideProps라는 함수를 사용했습니다.

- 그러나 App Router에서는 fetch 함수만 비동기로 사용해서 SSR을 구현합니다.

<03. Next.js 기초와 내장 컴포넌트>

- Next는 서버사이드 렌더링 외에도 많은 내장 컴포넌트와 함수를 제공합니다.

[3장에서는 다음과 같은 내용을 학습하게 됩니다.]

- 클라이언트와 서버에서의 라우팅 시스템 작동 방식

- 페이지 간 이동 최적화

- Next.js가 정적 자원을 제공하는 방법

- 자동 이미지 최적화와 새로운 image 컴포넌트를 사용한 이미지 제공 최적화 기법

- 컴포넌트에서 HTML 메타데이터를 처리하는 방법

- _app.js와 _documents.js 파일 내용 및 커스터마이징 방법

<3-1. 라우팅 시스템>

- React의 React Router, Reach Router 등은 클라이언트 라우팅만 구현할 수 있습니다.

- Next는 파일시스템 기반 페이지와 라우팅을 합니다.

- 페이지는 /pages 디렉토리 안의 *.js, *.jsx, *.ts, *.tsx 파일에서 export한 React 컴포넌트입니다.

        function Homepage() {
            return <div> This is the homepage </div>;
        }

        export default Homepage;

- 만일 블로그와 같이 컨텐츠를 분리해야 한다면 어떻게 해야 할까요?

- /pages 아래 디렉토리를 만들고 라우팅 규칙을 만들면 됩니다.

- /pages 디렉토리 내부에는 계층적 구조로 라우팅 규칙을 만들 수 있습니다.

- /pages/posts 안에 index.js와 [slug].js를 만들어 jsx를 반환합니다.

        pages/
            - index.js
            - contact-us.js
            - posts/
                - index.js
                - [slug].js

- /pages/posts/ 디렉토리 내에 Index.js만 간단하게 만들면 localhost:3000/posts로 접속이 가능합니다.

- 다만 동적인 라우팅 규칙을 만들려면 [slug].js 파일이 필요합니다.

- [slug].js는 매개 변수로 사용되며 주소창에서 입력하는 값을 모두 받을 수 있습니다.

- 동적 라우팅 규칙을 중첩할 수도 있습니다.

- 접근 경로를 ~/posts/[date]/[slug]와 같이 만들 수 있습니다.

- [date] 디렉토리를 만들고 그 안에 [slug].js 파일을 저장하면 됩니다.

- [date]나

<페이지에서 경로 매개변수 사용하기>

- 경로 매개변수를 사용해서 동적 페이지를 쉽게 만들 수 있습니다.

- page/greet/[name].js 파일을 만들어 보겠습니다.

- 내장 getServerSideProps 함수를 통해 URL에서 동적으로 [name] 변수 값을 가져오는 것입니다.

- greet/Mitch 주소로 가면 'Hello, Mitch!'라는 문구가 렌더링 됩니다.

        코드

- getServerSideProps나 getStaticProps 함수는 반드시 객체를 반환해야 합니다.

<컴포넌트에서 경로 매개변수 사용하기>

- pages 밖에서는 getServerSideProps나 getStaticProps 함수를 사용하지 못하는데, 어떻게 경로 매개변수를 컴포넌트 안에서 사용할 수 있을까요?

- useRouter Hook을 이용하면 컴포넌트 안에서 경로 매개변수를 사용할 수 있습니다.

- useRouter는 next/router