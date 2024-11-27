# 이주형 202030324
# 11월 27일 강의

<GitHub Pages 기본 저장소 생성>

- GitHub Pages를 운영하려면 먼저 GitHub 저장소를 생성해야 합니다.

- 생성 방법은 일반 저장소 생성과 동일하지만, 저장소 이름을 다음과 같이 해야 합니다.

- .home이 아니라 .io로 해야 합니다.
        
        <MyID>.github.io

<공용PC GitHub 인증 제거>

- 복수 계정을 사용하는 방법도 있지만 절차가 복잡하기 때문에 배포 연습은 글로벌 인증자료가 없는 상태에서 진행됩니다.

- 제어판 > 사용자 계정 > 자격 증명 관리 -> Windows 자격 증명 관리 에서

- Git 혹은 GitHub관련 인증을 모두 삭제합니다.

- user.name과 user.email을 global로 설정합니다.

        Bash
        
        $ git config --global user.name 'name'
        
        $ git config --global user.email 'user@sample.com'

<배포할 저장소와 프로젝트 생성>

- 앞서 <MyID>.github.io로 만든 저장소를 기본 저장소라고 한 이유는 이 저장소가 있어야
    나머지 저장소도 Page로 만들 수 있기 때문입니다.

- Working directory에 프로젝트를 새로 만들고, /page.js의 내용을 삭제 후 수정합니다.

- 간단한 라우팅 페이지를 몇 개 만들어 줍니다.

- 같은 이름으로 GitHub 저장소도 만듭니다.

- GitHub에서 Repositories 탭을 선택하고, 오른쪽 상단의 New버튼을 클릭합니다.

- 등록이 되었는지 확인합니다. remote를 확인하는 방법은 다음과 같습니다.

        Bash
        
        $ git remote -value
        
        origin https://github.com/jh2475/foo.git (fetch)

        origin https://github.com/jh2475/foo.git (push)

- 확인 결과가 정상적으로 등록되어 있지 않다면 삭제 후 다시 등록해 줄 수 있습니다.

- 이 명령은 터미널을 관리자 모드로 열어 실행합니다.

        Bash

        $ git remote remove origin

*** 사용자 등록이 되어 있지 않으면 commit도 되지 않습니다.

        Bash

        $ git config --global user.name 'name'

        $ git config --global user.email 'foo@example.com'

- Local로 돌아와서 프로젝트를 push합니다.

- 처음 push 할 때는 -u(upstream)옵션을 줍니다. 이렇게 하면 다음 부터는 git push만으로 push할 수 있습니다.

        Bash

        $ git push -u origin Main

- git을 설치하고 처음 push할 때는 인증을 하라는 창이 나옵니다.

- 파란색 버튼을 클릭하면 웹 브라우저에서 계정을 선택하거나 "Use a different account"를 클릭하여 로그인을 합니다.

- GitHub 저장소의 Settings > Pages의 Select branch에서 main(master)를 선택해 주세요.

- Save 버튼을 클릭합니다.

- 1~2분 후에 <id>.github.io/<Repo. name>으로 접속하면 readme를 확인할 수 있습니다.

<호스팅 비교>

- Github Page

1. 웹사이트: Github Page

2. 비용: 무료

3. 대역폭 제한: 매월 100GB (소프트 제한)

4. 저장 공간 제한: 게시된 사이트는 1GB 이하

5. 배포 시간 제한: 10분 이상 걸리면 시간 초과

6. 주요 특징: 간편한 Git 기반 배포

7. 관련 문서: Github Pages 정보 - 사용 제한

- Vercel

1. 비용: 무료 (Hobby 플랜)

2. 대역폭 제한: 100GB/월

3. 빌드 실행 제한: 월 6,000분

4. 주요 특징: 최신 프론트엔드 프레임워크 지원

- Netlify

1. 비용: 무료 (Starter 플랜)

2. 대역폭 제한: 100GB/월

3. 빌드 시간 제한: 월 300분

4. 주요 특징: 사용자 친화적인 UI와 강력한 배포 옵션

# 11월 20일 강의

<4. Context API vs. Redux>

[ Redux ]

- Redux는 전역 상태를 관리하기 위한 독립적인 state 관리 라이브러리입니다.

- 상태의 변경을 예측 가능하게 하고, 전역 state 관리를 더 구조적으로 지원합니다.

- store, reducer, action 등의 개념을 사용해 state와 state dispatch를 관리합니다.

( 장점 )

- 명확한 상태 관리 구조 : 액션과 reducer를 통해 state dispatch 과정을 예측 가능하게 만들고, 코드의 가독성을 높입니다.

- 미들웨어 지원 : redux-thunk, redux-saga와 같은 미들웨어를 사용해 비동기 로직을 쉽게 처리할 수 있습니다.

- 디버깅 도구 : Redux DevTools를 통해 상태 변화 및 디버깅이 용이합니다.

- 모든 프레임워크와 호환 : React뿐만 아니라 다른 JavaScript 프레임워크와도 함께 사용할 수 있습니다.

( 단점 )

- 설정과 코드 복잡도 : Context API에 비해 설정이 복잡하며, boilerplate 코드가 많이 필요합니다.

- 추가 라이브러리 필요 : Redux 자체가 외부 라이브러리이므로 설치 및 유지 관리가 필요합니다.

- 작은 애플리케이션에는 과한 설정 : 단순한 상태 관리가 필요한 작은 애플리케이션에서는 과도한 설정일 수 있습니다.

        항목        Context API     Redux
        
        규모        작은 규모       대규모

        복잡성      간단한 상태     복잡한 상태

        학습 난이도     낮음        높음

        성능        상황에 따라 다름        비교적 안정적

        유연성      낮음        높음

        디버깅 도구     기본적으로 없음     Redux DevTools 제공

<5. Redux (실습)>

2. counterSlice 파일을 생성합니다.

- createSlice로 Slice를 생성한 후 초기화와 reducers에 action을 설정해 줍니다.

- 여러 개의 Slice를 사용할 때도 name 필드의 값만 변경하고 그대로 사용하면 됩니다.

        import { createSlice } from "@reduxjs/toolkit";

        export const counterSlice = createSlice({
            name: 'counter', 
            initialState: {
                value: 0,
            },
            reducers: {
                increment: (state) => {
                    state.value += 1
                },
                decrement: (state) => {
                    state.value -=1
                },
            },
        })

        export const { increment, decrement } = counterSlice.actions
        export default counterSlice.reducer

3. store 설정 파일을 생성 합니다.

- store파일은 Redux 스토어를 설정하는 파일로, 기능별 Slice파일을 이곳에 등록합니다.

- 즉 모든 reducer를 한곳에 모아 중앙에서 관리하기 위한 파일입니다.

- 새로운 기능이 추가되면, 해당 기능의 Slice를 생성하고 등록합니다.

        import { configureStore } from "@reduxjs/toolkit";
        import counterReducer from '@/features/counter/counterSlice.jsx'

        export const store = configureStore({
            reducer: {
                counter: counterReducer,
            }
        })

4. Counter Component 파일을 생성합니다.

- useSelector는 Redux store의 상태를 선택(조회)하는 데 사용됩니다.

- 컴포넌트 내부에서 이 Hook을 사용하면 Redux store에서 필요한 state를 가져와 사용할 수 있습니다.

- useDispatch는 Redux store의 action을 디스패치(dispatch)하는 데 사용됩니다.

- 즉, Component에서 state를 변경하거나 업데이트할 때 이 Hook을 사용합니다.

- counterSlice에서 정의한 reducer를 호출하여, increment, decrement를 버튼에 적용합니다.

        'use client'
        import React from 'react'
        import { useSelector, useDispatch } from "react-redux"
        import { increment, decrement } from "./counterSlice"

        export function Counter() {
            const count = useSelector((state) => state.counter.value)
            const dispatch = useDispatch()

            return (
                <div>
                    <h1>{count}</h1>
                    <button onClick={() => dispatch(increment())}>Increment</button>
                    <button onClick={() => dispatch(decrement())}>Decrement</button>
                </div>
            )
        }

# 10월 25일 강의

<Json Server>

- Backend가 개발되기 전이나, 아직 외부 API가 결정되지 않았다면 local에 Json server를 구축하고 Frontend 개발을 하기에 적합한 node 패키지 입니다.

<Axios 란?>

- Next.js에서 REST API를 다룰 때는 보통 axios와 fetch 중 하나를 선택하는 경우가 많습니다.

[ Fetch API ]

- 내장 API: 브라우저에 내장되어 있어 별도의 설치가 필요 없습니다.

- Promise 기반: 비동기 작업을 처리하는 데 익숙한 구조입니다.

- 스트림 처리: 데이터를 스트리밍으로 처리할 수 있는 기능이 있어, 큰 파일을 처리하는 데 유용합니다.

단점은...

- json 변환 수동 처리: 응답에서 json으로 변환할 때 res.json()을 호출해야 합니다.

[ 결론 ]

- 복잡한 요청이나 에러 처리가 필요한 경우에는 axios가 더 적합할 수 있습니다.

- 간단한 요청이나 내장된 기능을 활용하고 싶다면 fetch를 사용하는 것도 좋은 선택입니다.

- 어떤 것을 선택할지는 프로젝트의 요구 사항과 개발자의 선호도에 따라 다를 수 있습니다.

# 10월 4일 강의

<Page Project Layout - app>

- _app.jsx는 서버에 요청할 때 가장 먼저 실행되는 컴포넌트입니다.

- 페이지에 적용할 공통 레이아웃을 선언하는 곳입니다.

- 기본 코드는 다음과 같습니다.

        import "@/styles/globals.css";

        export default function App({ Component, pageProps }) {
            return <Component {...pageProps} />;
        }

- Global CSS는 이곳에 추가 됩니다.

- props 중 Component는 서버에 요청한 페이지입니다.

- pageProps는 App.getInitialProps를 이용하여 prefetching된 데이터를 반환합니다.

- 데이터가 없다면 빈 객체({})를 반환합니다.

- 단, getStaticProps, getServerSideProps와 같은 Data Fetching methods는 동작하지 않습니다.

<Page Project Layout - document>

- _document.jsx는 _app.jsx 다음에 실행됩니다.

- 각 페이지에서 공통적으로 사용될 html, head, body 안에 들어갈 내용을 선언합니다.

- onClick 같은 이벤트나 CSS는 이 곳에 선언하지 않습니다.

- 만일 로직이나 스타일이 필요하다면 _app.jsx에 선언해야 합니다.

- 다음은 수정한 예입니다.

        import { Html, Head, Main, NextScript } from 'next/document'

        export default function Document() {
            return (
                <Html lang="ko">
                    <Head>
                        {/* 사용자 정의 메타 태그 */}
                        <meta name="description" content="커스텀 설명입니다."/>

                        {/* 외부 스크립트 추가 */}
                        <script src="..."></script>
                    </Head>
                    <body>
                        <Main/>
                        <NextScript/>
                    </body>
                </Html>
            )
        }

<App Project Layout - layout.jsx>

- layout.jsx는 app 디렉토리 아래에 위치합니다.

- layout.jsx는 Page Project에서 사용하던 _app.jsx와 _document.jsx를 대체합니다.

- 이 파일은 삭제해도 프로젝트를 실행하면 자동으로 다시 생겨납니다.

- 프로젝트를 생성할 때 생성된 기본 코드는 다음과 같습니다.

        export const metadata = {
            title: 'Next.js',
            description: 'Generated by Next.js',
        }

        export default Layout;

<App Project Layout - meta data>

        export const metadata = {
            title: {
                default: 'Next.js',
                template:
            }
        }

<Link vs. a vs. router.push>

- Link component를 이용해서 Navibar component를 만들어봅니다.

- a tag는 html 동기식으로 전체가 reload 되기 때문에, 외부 링크를 할 때 사용합니다.

- 일반적으로 내부 링크 이동시에는 사용하지 않는 것이 좋습니다.

- router.push는 빌드 후, 이동할 주소가 html 상에 노출되지 않기 때문에 SEO에 취약합니다.

- Link 컴포넌트는 빌드 후, a tag로 자동 변환됩니다.

- a tag의 장점인 SEO 최적화, prefetch 가능, 우 클릭 기능 등을 갖습니다.

- 내부 페이지로의 이동할 때 이 방식을 사용해야 SPA 방식으로 전체 html중 필요한 부분만 비동기식으로 리렌더링 된다.

<3.2 정적 자원 제공>

- 정적 자원은 이미지, 폰트, 아이콘, 컴파일한 css, js 등으로 /public 디렉토리 안에 저장합니다.

- 정적 자원 중 이미지 파일은 SEO에 많은 영향을 미칩니다.

- 불러오는데 많은 시간이 걸리고, 불러온 후에도 이미지 주변의 레이아웃이 변경되는 등 UX 관점에서 좋지 않은 영향을 줍니다.

- 이를 누적 레이아웃 이동( CLS: Cumulative Layout Shift)이라고 합니다.

- 사용자가 2번째 문단을 읽고 있었다면, 위치가 바뀌어서 읽던 곳을 놓칠 수 있습니다.

- image 컴포넌트를 사용해서 이와 같은 CLS문제를 해결합니다.

<자동 이미지 최적화>

- Next.js 10부터 Image 컴포넌트를 사용해서 이미지를 자동으로 최적화할 수 있습니다.

- 이 기능을 사용하면 이미지를 WebP와 같은 최신 이미지 포맷으로 제공할 수 있습니다.

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
        export async function getStaticProps() {
            const res = await fetch('https://api.github.com/repos/vercel/next.js')
            const repo = await res.json()
            return (
                props: { repo },
                    revalidate: 60,
                )       
        }

        export default function Chapter02_06({repo}) {
            return (
                <>
                    {/* Next 공식 문서 예제 */}
                    <div className={styles.center}>
                        {repo.name}
                    </div>
                </>
            )
        }

- Page Router에서는 SSR을 위해서 getServerSideProps라는 함수를 사용했습니다.

- 그러나 App Router에서는 fetch 함수만 비동기로 사용해서 SSR을 구현합니다.

<03. Next.js 기초와 내장 컴포넌트>

- Next는 서버사이드 렌더링 외에도 많은 내장 컴포넌트와 함수를 제공합니다.

[3장에서는 다음과 같은 내용을 학습하게 됩니다.]

- 클라이언트와 서버에서의 라우팅 시스템 작동 방식

- 페이지 간 이동 최적화

- Next.js가 정적 자원을 제공하는 방법

- 자동 이미지 최적화와 새로운 Image 컴포넌트를 사용한 이미지 제공 최적화 기법

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

- [date]나 [slug]는 어떤 값이든 가질 수 있습니다.

- 실제 앱에서는 경로 매개변수에 따라 서로 다른 동적 페이지를 렌더링하게 됩니다.

        pages/
            - index.js
            - contact-us.js
            - posts/
                - index.js
                - [date]/
                    - [slug].js

<페이지에서 경로 매개변수 사용하기>

- 경로 매개변수를 사용해서 동적 페이지를 쉽게 만들 수 있습니다.

- page/greet/[name].js 파일을 만들어 보겠습니다.

- 내장 getServerSideProps 함수를 통해 URL에서 동적으로 [name] 변수 값을 가져오는 것입니다.

- greet/Mitch 주소로 가면 'Hello, Mitch!'라는 문구가 렌더링 됩니다.

        export async function getServerSideProps({ params }) {
            const { name } = params;
            return {
                props: {
                    name,
                },
            };
        }

        function Greet(props) {
            return (
                <h1> Hello, {props.name}! </h1>
            );
        }

        export default Greet;

- getServerSideProps나 getStaticProps 함수는 반드시 객체를 반환해야 합니다.

<컴포넌트에서 경로 매개변수 사용하기>

- pages 밖에서는 getServerSideProps나 getStaticProps 함수를 사용하지 못하는데, 어떻게 경로 매개변수를 컴포넌트 안에서 사용할 수 있을까요?

- useRouter Hook을 이용하면 컴포넌트 안에서 경로 매개변수를 사용할 수 있습니다.

- useRouter는 next/router에서 가져올 수 있습니다.

- useRouter Hook을 사용해서 query 매개 변수를 가져옵니다.

- 콘솔에 로그를 출력하면 매개 변수와 쿼리 문자열들을 어떻게 전달하는지 알 수 있습니다.

- greet/Mitch?foo=true로 접속하여 log를 확인해 봅니다.

        import { useRouter } from 'next/router';

        function Greet() {
            const { query } = useRouter();
            console.log(query);
            return <h1>Hello {query.name}!</h1>;
        }

        export default Greet;

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

- 리액트 하이드레이션 덕분에 이 상태에서 웹 앱은 싱글 페이지 애플리케이션(SPA) 처럼 작동할 수 있습니다.

- CSR과 SSR의 장점을 모두 가지는 것입니다.

- 특정 렌더링 전략만 사용한다고 가정하면 SSR이 CSR에 비해 여러 가지 장점이 있습니다.

<서버 사이드 렌더링(SSR)>

- 생소할 수도 있지만 웹 페이지를 제공하는 가장 흔한 방법입니다.

- APM을 이용하는 일반적인 웹 페이지 생성이라고 보면 됩니다.

- 여기에 자바스크립트 코드가 적재되면 동적으로 페이지 내용을 렌더링합니다.

- Next.js도 이와 같이 동적으로 페이지를 렌더링할 수 있습니다.

- 그리고 여기에 스크립트 코드를 집어 넣어서 나중에 웹 페이지를 동적으로 처리할 수도 있는데 이를 하이드레이션이라고 합니다.

- 예를 들면 어떤 사람이 작성한 블로그 글을 한 페이지에 모아서 작성해야 한다면 SSR을 이용하는 것이 적당합니다.

- 서버 사이드 렌더링 -> 자바스크립트가 화이드레이션된 페이지를 전송 -> 클라이언트에서 DOM 위에 각 스크립트 코드를 하이드레이션 : 페이지 새로 고침 없이 사용자와 웹 페이지간 상호 작용을 가능하게 합니다.

[ SSR의 장점 ]

- 더 안전한 웹 애플리케이션: 쿠키 관리, 주요 API, 데이터 검증 등과 같은 작업을 서버에서 처리하기 때문에 중요한 데이터를 클라이언트에 노출할 필요가 없기 때문입니다.

- 더 뛰어난 웹 사이트 호환성: 클라이언트 환경이 자바스크립트를 사용하지 못하거나 오래된 브라우저를 사용하더라도 서비스를 제공할 수 있습니다.

- 더 뛰어난 SEO: 서버가 렌더링한 HTML을 받기 때문에 봇이나 웹 크롤러가 페이지를 렌더링할 필요가 있기 때문입니다.

<SSR이 최적의 렌더링 전략이 아닌 경우>

- 클라이언트가 페이지를 요청할 때마다 페이지를 다시 렌더링할 수 있는 서버가 필요합니다.

- 다른 방식에 비해 SSR이 더 많은 자원을 소모하고, 더 많은 부하를 보이며 유지 보수 비용도 증가합니다.

- 페이지에 대한 요청을 처리하는 시간이 길어집니다.

- 페이지가 외부 API 또는 데이터 소스에 접근해야 한다면, 해당 페이지를 렌더링할 때마다 이를 다시 요청해야 합니다.

- 페이지 간의 이동은 CSR에 비해 느립니다.

- 중요한 것은 Next.js가 기본적으로 빌드 시점에 정적으로 페이지를 만든다는 것입니다.

- 페이지에서 외부 API를 호출하거나 데이터베이스에 접근하는 등 동적 작업을 해야 한다면 해당하는 함수를 페이지에 export해야 합니다.

<코드 설명(36P)>

- 이 페이지는 div 요소 안에 문자열만 표시합니다.

- 외부 API를 호출 하지 않으며 항상 같은 문자열만 표시됩니다.

        function IndexPage() {
            return <div>This is the index page.</div>;
        }

        export default IndexPage;

- 다음 코드는 페이지를 요청할 때마다 사용자 환영 문구를 표시합니다.

- 특정 사용자 정보를 가져온 다음 클라이언트에 전달해서 사용할 수 있도록 하고 있습니다.

- 이 경우 미리 예약된 getServerSideProps() 함수를 사용합니다.

        export async function getServerSideProps() {
            const userRequest = await fetch('https://example.com/api/user');
            const userData = await userRequest.json();

            return {
                props: {
                    user: userData,
                },
            };
        }

        function IndexPage(props) {
            return <div>Welcome, {props.user.name}!</div>;
        }

        export default IndexPage;

- 페이지에 대한 요청이 들어오면 서버가 REST API를 호출해서 필요한 사용자 정보를 가져옵니다.

- 이 과정은 다음과 같은 세부 단계로 나눌 수 있습니다.

1. getServerSideProps라는 비동기 함수를 export합니다. 빌드 과정에서 Next.js는 이 함수를 export하는 모든 페이지를 찾아서 서버가 페이지 요청을 처리할 때 getServerSideProps 함수를 호출하도록 만듭니다.

2. getServeerSideProps 함수는 props라는 속성값을 갖는 객체를 반환합니다. 이 props는 컴포넌트로 전달돼 서버와 클라이언트 모두가 props에 접근할 수 있게 됩니다. fetch API는 서버에서 실행되기 때문에 별도의 폴리필을 끼워 넣을 필요는 없습니다.

3. IndexPage 함수를 수정해서 props를 인자로 받습니다. 이 props는 getServerSideProps함수에서 반환한 props의 모든 내용을 갖고 있습니다.

- 14부터는 하나의 API만 사용합니다.

<Next.js 13 vs 14>

- Pages Router -> App Router

- Data Fetching: 13까지는 getServerSideProps, getStaticProps 메소드를 이용해서 구현 했으나, 14에서는 SSG(정적 사이트 생성), SSR(서버측 렌더링) 및 ISR(증분적 정적 재생성)에서 하나의 API만을 사용해서 구현할 수 있게 되었습니다.

        // This request should be cached until manually invalidated.
        // Similar to `getStaticProps`.
        // `force-cache` is the default and can be omitted.
        fetch(URL, { cache:'force-cache'});

        // This request should be refetched on every request.
        // Similar to `getServerSideProps`.
        fetch(URL, { cache:'no-store'});

        // This request should be cached with a lifetime of 10 seconds.
        // Similar to `getStaticProps` with the `revalidate`option.
        fetch(URL, { next: { revalidate: m}});

- Turbopack: Rust 기반으로 개발된 새로운 번들러 사용으로 webpack보다 700배 빠르다고 발표했습니다.

- Turbopack은 3,000개의 모듈이 있는 애플리케이션에서 1.8초만에 부팅되고, Webpack은 6.5초, Vite는 11.4초가 걸립니다.

<CSR을 사용할 때의 주요 이점>

[네이티브 앱처럼 느껴지는 웹 앱]

- 전체 자바스크립트 번들을 다운로드 한다는 것은 렌더링할 모든 페이지가 이미 브라우저에 다운로드 되어 있다는 뜻입니다.

- 다른 페이지로 이동해도 서버에 요청할 필요 없이, 바로 페이지를 이동할 수 있습니다.

- 페이지를 바꾸기 위해 새로 고칠 필요가 없습니다.

[쉬운 페이지 전환]

- 클라이언트에서의 내비게이션은 브라우저 화면을 새로 고칠 필요 없이 다른 페이지로의 이동을 가능하게 만듭니다.

- 페이지 간 전환에 멋진 효과를 넣을 수도 있습니다. 애니메이션을 방해할 요소가 없기 때문입니다.

[지연된 로딩과 성능]

- 웹 앱은 최소로 필요한 HTML만 렌더링합니다.

- 버튼을 누르면 나오는 모달도 실제 버튼이 늘렸을 때 동적으로 생성하게 됩니다.

[서버 부하 감소 - 서버리스 환경에서 웹 앱을 제공할 수도 있습니다.]

<장점은 단점이 될 수도 있습니다.>

- 네트워크 속도가 느린 환경에서는 번들이 모두 다운로드 될 때까지 계속 빈 페이지를 보아야 합니다.

- 검색 로봇에게도 그 내용은 빈 것으로 보입니다.

- 번들을 모두 받을 때까지 검색 로봇이 기다리기는 하지만 성능 점수는 낮을 것입니다.

- React.useEffect Hook

- 최근 리액트는 함수형 컴포넌트 사용을 강조하면서 life cycle함수 대신 Hook을 사용합니다.

- 함수형 컴포넌트 내에서 DOM조작이나 데이터 불러오기 같은 사이드 이펙트 기능을 구현할 때, useEffect함수를 사용해서 컴포넌트가 마운트된 후 해당 기능을 실행하도록 만들 수 있습니다.

- 다음과 같이 React.useEffect와 React.useState를 함께 써서 특정 컴포넌트를 정확히 클라이언트에서만 렌더링하도록 지정할 수 있습니다.

        import {useEffect, useState} from 'react';
        import Highlight from '../components/Highlight';

        function UseEffectPage() {
            const [isClient, setIsClient] = useState(false);

            useEffect(() => {
                setIsClient(true);
            }, []);

            return (
                <div>
                    {isClient && 
                        (<Highlight
                            code={"console.log('Hello, world!')"}
                            language='js'
                        />)
                    }
                </div>
            );
        }

        export default UseEffectPage;

<2.3 정적 사이트 생성(SSG: Static Site Generation)>

- SSG는 일부 또는 전체 페이지를 빌드 시점에 미리 렌더링 합니다.

- SSG는 SSR 및 CSR과 비교했을 때 다음과 같은 장점이 있습니다.

1. 쉬운 확장

    정적 페이지는 단순 HTML 파일이므로 CDN을 통해 파일을 제공하거나, 캐시에 저장하기 쉽습니다.

2. 뛰어난 성능

    빌드 시점에 HTML 페이지를 미리 렌더링하기 때문에 페이지를 요청해도 클라이언트나 서버가 무언가를 처리할 필요가 없습니다.

3. 더 안전한 API 요청

    외부 API를 호출하거나, 데이터베이스에 접근하거나, 보호해야 할 데이터에 접근할 일이 없습니다.
    
    필요한 모든 정보가 빌드 시점에 미리 페이지로 렌더링 되어 있기 때문입니다.

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