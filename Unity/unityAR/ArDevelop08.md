# Unity (유니티)  
## 유니티로 AR 정복하기  
### Load Scene 코딩 (2023.03.28)  
유니티 프로젝트에서 Scene을 여러개 생성하여 옮겨다니면서 여러 기능들을 사용할 수 있다.  
보통 한 Scene에서 하나의 기능을 구현해놓고, Scene들을 Load하는 코딩을 통해 여러 Scene을 사용한다.  
이번엔 그 UI를 제작해보는 실습이다.  
모든 Scene마다 굳이 AR Session을 항상 넣을 필요는 없다.  
Scene의 작업테이블에 Canvas를 생성하고 Panel을 생성한뒤 그 내부에 Button UI를 만들어줬다.  
Panel에 Grid Layout Group이라는 컴포넌트를 추가해주니 Grid 규격에 맞게 버튼이 정리된다.  
각각의 셀사이즈나 셀사이의 거리는 Grid Layout Group 설정으로 조절할 수 있다.  
버튼의 정렬을 설정할 수도 있다. Rect Transform 설정에서 margin을 설정할 수 있다.  
버튼의 색이나 버튼 내부의 Text 사이즈 및 색상 변경도 가능하다.  

버튼을 만들었으면 버튼을 사용해서 다른 Scene으로 이동하는 기능을 추가할 수 있을 것이다.  
버튼 속성에 OnClick()이라는 함수가 있다. 클릭할 때마다 어떤 기능을 수행할지에 관한 것이다.  
먼저 Empty를 Create하면 기본적으로 GameObject가 생성된다.  
이 이름을 ARSceneManager로 변경해주고 스크립트가 짜인 컴포넌트를 통해 Scene 이동을 관리할 것이다.  

Script의 라이브러리에 using UnityEngine.SceneManagement; 를 등록한다.  
이 Script에는 start함수와 update함수는 필요가 없기에 삭제해도 된다.  
Scene 이동은 코딩이 단순하다.  
Scenemanager.LoadScene("Scene 이름", LoadSceneMode 설정); 으로 불러온다.  
LoadSceneMode에는 Single과 Additive가 있다.  
Single은 기존의 Scene이 닫히고 새로 열리는 것이고, Additive는 기존의 Scene이 뒤덮이는 방식이다.  

먼저 대규모 공사.. 기존에 있던 프로젝트들을 전부 Scene만 데려와서 MyUnity 프로젝트에 전부 합쳐주었다.  
우리가 LoadScene메소드에서 string 타입으로 Scene의 이름을 불러와서 Load했었다.  
참고로 Build Setting에 있는 Scene의 index번호값을 보고 그 번호값을 넣어도 Scene이 불러와진다.  
LoadSceneMode를 Single이 아닌 Additive로 하게되면 씬이 중첩해서 돌게되는데,  
각각 Scene마다 우리는 AR Session을 넣어두었을 텐데 이들이 사라지지 않고 중첩되다보면 분명 오류가 나기 쉽다. (과부하)  
또한 이전 Scene의 객체가 계속 남아있는 문제가 생길수도 있다.  
따라서 Additive를 쓰기 위해선 Scene이 보이지 않을때 컨텐츠를 정리하는 코드까지 고려해야한다.  

나는 GameObject 생성해서 뒤로가기 기능 추가했다.
