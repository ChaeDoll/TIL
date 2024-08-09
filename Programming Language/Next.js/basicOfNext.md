# Next.js는 무엇인가

## React 기반 풀스택 프레임워크
- React는 클라이언트 렌더링으로서 모든 javascript 파일을 로드하고 사용하는 웹을 보게됨 (이때 시간지연)
- 따라서 javascript가 없으면 동작하지 않는 웹임
- Next.js는 서버 렌더링을 사용하여 서버측에서 html과 css를 만들어 띄워주는 형식임
- style jsx 또는 style jsx global 이라는 태그를 통해 해당 컴포넌트에 적용되는 css를 가질 수 있다. global은 말그대로 글로벌
- next.js에 있는 Link태그를 통해 SPA(Single Page Application)을 구현할 수 있다.
- 동적 url을 편리하게 적용할 수 있다. (예: /read/1... /read/361)
- react에 있는 기능들을 거의 유사하게 사용가능하다 (예시로 Router)
- **SPA를 편리하게 지원하고, 완전한 서버렌더링 애플리케이션 제작이 가능하여 백엔드 프레임워크가 필요하지 않다**
- 프론트와 백엔드를 통합하여 관리하기 편하다는 장점이 Next.js를 쓰게 된 주요 목적이다.

### 명령어
- npx create-next-app@latest . : 현재 디렉토리에 next app 설치
- npm run dev : 개발중인 내용을 기반으로 실행
- npm run build : 개발한 내용을 build
- npm run start : 빌드된 내용을 기반으로 실행

### 기초 코드
- 앱이 실행되면 src/app/layout.js가 실행됨
- 이 내부에서 head의 metadata들과 레이아웃을 수정할 수 있음 (기본 틀)
- layout은 children이라는것을 받아서 body에 출력한다. 이것이 내용
- src/app/page.js 에 있는 내용들이 return 되어 children에 들어간다.
- src/app/global.css 에 있는 내용들이 layout.js를 포함한 모든 내용에 적용되는 css이다.
- 레이아웃은 고정된 상태로, page에 있는 내용들을 변경시키는 것이 일반적.
- 새로운 페이지를 만들고 싶다면 src/app/ 경로에 새로운 폴더를 만들고 (페이지명) 그 내부에 page.js 혹은 layout.js를 만들면 그 폴더명의 페이지 내용을 담을수도 있고, 메인레이아웃에 추가적으로 들어가는 layout도 만들 수 있다.
- 폴더 내부의 page.js는 기본적으로 같은 디렉토리 내의 layout.js에 들어가지만, 같은 디렉토리 내에 layout이 없다면 부모폴더의 layout에 들어간다.
- 동적라우팅은 read/1 , read/2 처럼 같은 페이지 내의 다른 경로들을 다루는 방법이다
- 폴더를 만들 때 src/app/read를 만들고 그 내에 [id] 라는식으로 폴더를 만든뒤 그 내에 page.js를 만들면 된다.
- 그 내에서는 props를 사용하여 {props.params.id}라는 구문을 통해 주소값으로 입력된 id값을 불러와 사용할 수 있게된다.
- 그 값을 조리있게 사용하여 동적으로 페이지를 출력하면 된다.
- Link를 사용하면 SPA를구현할 수 있다. 컴포넌트도 Link가 향하는 페이지 컴포넌트만 적용된다.
- public 폴더 내에 이미지들을 삽입하면 정적자원사용이 가능하다. img src='/'가 public임
- 

---여기까지 230803---