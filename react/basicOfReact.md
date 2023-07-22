# 리액트 (React)
## 중요 명령어
- npx create-react-app '프로젝트명' : React 프로젝트 생성 (node.js가 설치되어있어야 함)
- npm init react-app '프로젝트명' : initializier
- cd '프로젝트명' : 프로젝트 내부로 이동 시에는 프로젝트명으로 cd한다
- npm start : Project 내부에서 실행 시 React Project 실행
- npm test : Project를 테스터에 돌려서 오류가 있는지 확인
- npm run build : build 폴더 내부에 제작한 앱의 최적화된 Build 생성

- npm install -g serve : serve 패키지 다운
- npx serve -s build : 임시 서버 빌드

## 코딩
- Project를 생성하고 내부에 접근하면, public 폴더와 src 폴더가 있다.  
- 실질적으로 수정할 부분은 src 폴더 내부 --> App.js --> < div className="App" > 내부 공간이다.
- CSS의 수정은 src 폴더 내부에 있는 'index.css' 파일이다.

## package.json 수정
- "homepage": "홈페이지 주소", 를 추가하여 주소에 React 프로젝트 연결 가능
- 사용 포트 변경 - 우선 scripts의 start에서 "set PORT='포트번호' && react-scripts start" 으로 변경,  
Project 폴더 내의 node_modules/react-scripts/scripts/start.js 에서 DEFAULT_PORT 수정,  
Project 폴더 내에 .env 파일 만들고 PORT='포트번호' 작성 후 저장