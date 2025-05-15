**라이브러리와 프레임 워크 차이**
라이브러리는 우리가 필요한 걸 import해서 사용하는 거고, 프레임워크는 형식에 맞춰서 우리의 코드를 입력하면 원하는 결과로 바꿔준다.
- 라이브러리는 사용자가 라이브러리를 호출하는 것이고,
- 프레임워크는 프레임워크가 코드를 호출하는 것이다.

**시작 과정**
1. 폴더 만들고 npm init -y `npm 설치`
2. npm i react@latest next@latest react-dom@latest `react, nextjs 설치`
3. package.json에서 script에 "dev" : "next dev" 코드 추가 `next js 시작 명령어`
4. app폴더 - page.jsx 파일 만들고 리액트 형식으로 코드 작성
5. npm run dev로 실행
패키지 설치 과정에서 node버전이 낮아 오류가 났었다. 컴퓨터에 설치되어 있는 nvm을 통해 최신버전을 설치했더니 이미 설치되어 있다고 해서 사용을 해줬다.
![[첨부 파일 소스/Image File 1/Pasted image 20240405193035.png]]
![[첨부 파일 소스/Image File 1/Pasted image 20240405193043.png]]

**Next js의 라우팅 과정**
기존 react에서 라우터를 통해 URL과 컴포넌트를 지정해서 수동으로 지정하지만,
Next js에서는 폴더 트리를 통해서 구성한다. 이동하고 싶은 주소의 이름을 폴더로 만들고, 해당 폴더 안에 page.jsx 파일을 만들면 해당 폴더를 경로로 인식한다.

`예: localhost:3000/items/cups 경로의 페이지를 만들고 싶으면, app폴더 안에 items폴더를 생성하고 그 안에 page.jsx 파일을 만든 뒤 items폴더 안에 cups폴더와 page.jsx파일을 생성한다.` 
![[첨부 파일 소스/Image File 1/Pasted image 20240331153553.png]]
폴더 내부에 page파일이 없으면 해당 폴더는 경로로 인식하지 않는다.
page파일 안에 export 이름은 원하는 이름으로 설정.

**Routes만들기**
Next js에서 원하는 페이지로 이동하려면 next에 내장되어있는 Link 컴포넌트를 사용하여 이동할 수 있다.
![[첨부 파일 소스/Image File 1/Pasted image 20240402175952.png]]
![[첨부 파일 소스/Image File 1/Pasted image 20240402180022.png]]
이동하고 싶은 경로를 href에 적으면 됨.

현재 페이지의 경로를 알고 싶으면 usePathname사용
![[첨부 파일 소스/Image File 1/Pasted image 20240402180126.png]]
![[첨부 파일 소스/Image File 1/Pasted image 20240402180133.png]]
![[첨부 파일 소스/Image File 1/Pasted image 20240402180148.png]]
usePathname을 활용하여 navbar에서 현재 페이지 표시.

**not-found**
app폴더에 not-found.jsx 를 통해서 잘못된 경로에 대한 페이지를 만들 수 있다.

**CSR vs SSR**
- 기본 React에서는 CSR(Clinet Side Rendering)을 사용하는데, CSR은 웹 페이지를 로드할 때 처음에는 빈 페이지였다가, 사용자가 접속할 때 javascript를 사용하여 html로 바꿔주어 로드한다. 이로인해 초기 로딩시간이 걸릴 수 있으며 SEO검색엔진에 내용이 인식되지 않는다.
- Next js에서 사용하는 SSR(Server Side Rendering)은 백엔드에서 Render하여 코드를 html로 변환하여 브라우저에 전달하기 때문에, javascript를 사용하지 않고도 로드한다. 때문에 초기 화면에 이미 html로 내용이 다 구성되어있기 때문에 검색 엔진으로 인식하는 데에도 문제가 없다.

**Hydration**
단순 HTML을 React application으로 초기화하는 작업.
next js로 만든 사이트를 사용자가 처음 접속할 때, 사이트에는 단순 HTML만 있는 상태이다. 접속하고 나서 빠른 속도로 React application이 작동하면서 단순 HTML구문을 리액트 구문으로 바꿔주어 interactive하게 작동하게 만들어준다.

Javascript를 끄고 페이지에 들어가면 단순 html로 구성된 페이지라 링크를 클릭할 때마다 페이지가 새로고침 되지만, javascript를 키면 react application으로 초기화되어 새로고침 없이 다른 페이지로 로드된다.
*"use client"* 명령어가 있는 component만 hydrate된다.

**use client**
next js에서 "use client"를 사용하지 않는 컴포넌트들은 server rendering만 된다.
즉, server에서 html로 로드하고 hydration과정을 거치지 않는다는 의미다.
이를 통해서 단순 html구현만 필요한 component의 경우에는 사용자가 불필요하게 javascript코드를 다운받지 않아도 되어 더욱 효율적으로 페이지를 로드할 수 있다.

**Layouts**
app폴더에 자동으로 생성되는 layout.js파일을 통해서 하위 폴더에 있는 모든page에 내용을 넣을 수 있다. {children}은 해당 페이지에 있는 정보를 의미함.
경로별로 개별 layout을 만들어 줄 수도 있는데, 어떤 폴더에 layout파일을 만들면 하위 폴더에 있는 모든 page에 layout이 적용된다.

**Groups**
폴더 이름을 ( )로 묶으면 경로로 인식되지 않는다.

**Metadata**
layout파일을 통해 metadata를 넘겨주는데, 페이지마다 개별적으로 meta를 설정해 줄 수 있다. 해당 page.jsx파일에서 내보내고 싶은 metadata를 export하면 기존 metadata에 중첩되어서 적용된다. 단, client rendering 페이지에서는 Metadata를 export할 수 없다.
![[첨부 파일 소스/Image File 1/Pasted image 20240402205329.png]]
![[첨부 파일 소스/Image File 1/Pasted image 20240402205348.png]]
- title에는 문자뿐만 아니라 템플릿을 적용시킬 수도 있다.

**Dynamic Routes**
Next js에서는 동적 페이지를 쉽게 적용할 수 있다. 예를 들어 movies페이지 중에 영화별로 id를 받아와서 movies/112341 이렇게 id별 페이지로 이동하는 동적 경로를 구성하고 싶으면, 경로 폴더에 [ id] 대괄호 안에 id를 넣어주면 된다.
![[첨부 파일 소스/Image File 1/Pasted image 20240402205642.png]]

![[첨부 파일 소스/Image File 1/Pasted image 20240402205717.png]]
- 또한 경로의 id를 가져와서 사용 가능하다.

경로는 id하나만 받는게 아니라, movies/2nd?region=kr 이렇게 여러개가 있는 경우도 받아올 수 있다.
![[첨부 파일 소스/Image File 1/Pasted image 20240402205831.png]]

**Data Fetch**
Client Side형식의 data fetching과정을 Server Side 형식으로 바꾸기.

![[첨부 파일 소스/Image File 1/Pasted image 20240404014308.png]]
react에서 사용하는 client형식의 fetch과정. client형식이기 때문에 metadata또한 내보내지 못한다.

![[첨부 파일 소스/Image File 1/Pasted image 20240404014907.png]]
백엔드에서 fetch 데이터를 가져오기 때문에 사용자가 API관련된 코드를 볼 수 없는게 이점으로 작용.

그렇다고 반드시 "use client"를 사용해선 안된다는 뜻은 아니다.

**Loading Components**
loading파일을 통해 프레임워크가 자동으로 로딩 화면 구성.
![[첨부 파일 소스/Image File 1/Pasted image 20240404202945.png]]
이처럼 같은 경로에 있는 page파일에 대해 loading파일이 자동적으로 로딩 화면 구성. 페이지에 접속하면 layout파일을 읽고 먼저 ui를 구현한 다음, 백엔드에서 데이터를 처리하는 동안 loading파일을 띄워줌. 데이터 처리가 완료되면 loading파일에서 page파일로 바꿔서 출력. 

**Parallel Requests**
비동기 함수 병렬적으로 처리하기.
![[첨부 파일 소스/Image File 1/Pasted image 20240404221731.png]]
동시에 시작하는 대신에 실행이 모두 끝날 때 까지 기다려야 한다는 단점이 있음.

**Suspense**
![[첨부 파일 소스/Image File 1/Pasted image 20240404230326.png]]
Data Fetching과정에서 Parallel Requests처럼 데이터가 묶이는 단점을 해결하기 위해 개별 컴포넌트로 분리해서 데이터를 처리함.

![[첨부 파일 소스/Image File 1/Pasted image 20240404230258.png]]
- `MovieVideos를 따로 컴포넌트로 분리한 모습.`
이렇게 처리하면 MovieVideos함수 또한 비동기 함수이므로 불러올 때 비동기 처리를 해줘야 하는데, react에서 사용하는 Suspense를 통해 처리해준다.

![[첨부 파일 소스/Image File 1/Pasted image 20240404230429.png]]
fallback을 통해서 로딩 중에 보여줄 문자도 만들어줄 수 있다.

Suspense를 사용하면 Data fetching 개별적으로 처리할 수 있어서, 먼저 처리되는 데이터별로 화면에 출력될 수 있도록 만들어준다.

**Error handling**
![[첨부 파일 소스/Image File 1/Pasted image 20240404233347.png]]
error파일을 만들어서 에러 발생 시에 애플리케이션 전체에 에러가 나는 것을 방지하고 해당 페이지에만 지정해둔 에러메시지와 에러 팝업을 실행시킬 수 있게 만들어준다.

**CSS Modules**
Next js에서는 CSS프레임워크들을 임포트 하지 않고도 사용할 수 있다.
또한 global.css파일을 통해 전체 페이지에 css를 적용할 수 있음.
페이지나 특정 부분에 CSS를 적용할 때는 CSS modules을 사용하는데, CSS이름뒤에 반드시 .modules.css가 붙어야 한다.![[첨부 파일 소스/Image File 1/Pasted image 20240405015112.png]]
앞에 이름인 navigation과 파일 위치는 상관 X

![[첨부 파일 소스/Image File 1/Pasted image 20240405015204.png]]]
CSS내부에는 ClassName으로 지정하고,

![[첨부 파일 소스/Image File 1/Pasted image 20240405015220.png]]
![[첨부 파일 소스/Image File 1/Pasted image 20240405015228.png]]
page파일에서는 js파일처럼 css파일을 import해와서 className을 지정해서적용한다.
이렇게 적용하게 되면 다른 코드나 페이지에 css가 잘못 적용되는 경우를 방지할 수 있음.

![[첨부 파일 소스/Image File 1/Pasted image 20240405164943.png]]
![[첨부 파일 소스/Image File 1/Pasted image 20240405165002.png]]
데이터별로 CSS module을 통해 css적용하는 과정.

**Dynamic Metadata**
id에 따라 페이지가 바뀌는 동적 경로에서 metadata 동적으로 내보내기.
![[첨부 파일 소스/Image File 1/Pasted image 20240405165414.png]]
![[첨부 파일 소스/Image File 1/Pasted image 20240405165451.png]]
movie-info 컴포넌트에 있는 api fetching과정을 export하고 page에서 가져온다.

![[첨부 파일 소스/Image File 1/Pasted image 20240405165511.png]]
meatadata에서도 id를 똑같이 받아와서 제목을 지정해줌.

**page export**
page에서는 정해진 것들만 export 할 수 있음. 그렇기 때문에 API_URL을 export해서 에러가 났었는데, 따로 파일을 만들어서 거기에서 export해야 함.

**Vercel**
Vercel을 통해서 깃허브와 연동하기만 하면 깃허브에서 레포지토리를 가져와서 배포할 수 있음.

![[첨부 파일 소스/Image File 1/Pasted image 20240405182553.png]]
Link에 prefetch를 추가해서 사용자가 홈페이지에 접속하면, 클릭하지 않은 홈페이지에 있는 데이터도 자동으로 로딩을 진행시켜서 다른 페이지에 접속했을 때 로딩시간이 길어지는 걸 방지해줌.



## Movie프로젝트

![[첨부 파일 소스/Image File 1/Pasted image 20240408171121.png]]
함수에서 인수로 받아올 때 { }로 감싸는거 잊지 않기.

![[첨부 파일 소스/Image File 1/Pasted image 20240408173515.png]]
비동기 함수를 불러올때는 불러오는 함수에도 async await 붙이기