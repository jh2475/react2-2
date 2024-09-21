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