# K-MOOC 유니티 VR 프로그래밍 실습 강의 나만의 총 정리
- 물체의 Collider를 넣을 때는 요소들 각각에 Collider를 넣어야함. (전체를 묶는 그룹에 Collider넣으면 X)
- 키보드의 V키를 누르면서 물체를 움직이면 다른 물체에 붙여서 움직일 수 있음 
- 판, 네모와 같은 Mesh는 BoxCollider를 적용, 크기를 조절할 수도 있다.
- 망, 링 등은 Mesh Collider를 사용하는데, Convex라는 버튼을 누르면 원하는대로 작동하지 않을 수 있으니 주의
- Collider과 RigidBody Component를 함께 사용하면 Physics가 적용된 Object로 사용할 수 있다.
- 공을 만들었는데, 이 공을 바닥에 튀기고 싶다면 Physic Material 이라는 요소를 생성하여 Bounce(충돌)시, Friction(마찰)시에 요소를 조절가능
- UI를 만들려면 먼저 Canvas를 우클릭->UI->Canvas로 만들어주고, 해당 Canvas안에 Create Empty를 만들고 그 안에 UI적 요소 (Text, Button, Image)등을 넣는게 일반적
- Scene 간의 이동을 구현하고 싶다면 스크립트에서 SceneManager라는 namespace를 using하여 사용할 수 있음.
- class를 script로 만들고 method도 정의했다면, Hierarchy에 Empty를 만든뒤 Script를 넣어 객체화 시킬 수 있음
- Scene 간의 이동을 위해 BuildSetting 내에 Scene을 추가해놓으면 이제 SceneManager가 해당 Scene의 이름들을 통해 Load할 수 있음
- Input.GetKey(KeyCode.키)는 해당 Key를 누를때 boolean으로 답하는 메소드임. GetKeyDown과 GetKeyUp도 있다. (누를때 땔때 작동)
- 스크립트에서 GameObject 변수를 public으로 선언했다면 유니티 창의 Inspector에서 해당 변수에 직접 GameObject를 넣을 수 있음.(드래그앤드롭)  
그리고 이렇게 넣은 GameObject를 사용하는 코드를 스크립트 안에 만들어 둔다면, 이것이 바로 유니티의 요소들을 조작하는 방법임
- GameObject에 Component들에 접근하는 방법도 있음. 인스턴스를 만들었다면, a.GetComponent<컴포넌트명>().속성명 으로 해당 컴포넌트와 속성에 접근이 가능함
- 변수는 public으로 정의 시 유니티 Inspector에서 조작할 수 있고 (값 변경 가능), private으로 하면 변경 불가능할듯.
- OnCollisionEnter 혹은 OnTriggerEnter는 각각 '물체가 충돌했을 때', '물체가 영역이 겹칠 때'를 의미함. 각 이벤트변수.gameObject.tag를 통해 해당 이벤트가 일어난 object의 tag를 알 수 있음.  
그 tag는 우리가 직접 설정해주어야 한다. (Custom Tag도 만들수있음)
- 내가 스크립트를 짜고, 해당 스크립트를 EmptyObject에 넣은것이 Hiereachy에 존재할 때,  
다른 스크립트에서도 해당 스크립트에 접근할 수 있다. private 클래스명 instance;로 선언하고 void Start()안에서 GameObject.Find("Hiererachy에 있는 이름").GetComponent<"넣어놓은스크립트이름">();으로  
해당 스크립트를 가져올 수 있고, 이를 위에서 선언한 instance에 대입하여 초기화시키면 된다.


## 학습정보 정리
- 2D,3D assets을 import하는 방법 배움
- Materials를 만들고 Collider를 넣음, RigidBody와 Collider를 통해 Physic Material도 구현함
- first Person Camera, Unity 각도 왼손의 법칙 (왼손으로 엄지를 치켜세우고 방향을 가르키면 손의 방향으로 +회전이라는걸 알 수 있음)을 이해
- 실제 스크립트(C#)를 통해 Method, InputManager, Local Move, Time.deltaTime(frame에 관계없게 하는방법) 을 이해
- Scene Management, Menu (UI), Image와 Sprite, Canvas Scalar 를 배움
- F를 눌러 Focus하는 방법을 알고 Grid Snapping이라는게 있다는걸 알음(근데 난 없던데)
- Anchor와 alt를 누르며 고정. Canvas, Text, Button과 같은 UI요소 이해. Debud.Log를 통한 디버깅 이해
- OnClick메소드, SetActive(bool)메소드 이해 및 사용
- Build Setting, Esc키를 통한 Toggle Menu 구현, public GameObject 선언 및 활용, Input.GetKey(KeyCode)를 통한 입력받기 이해 및 활용
- Player Script 작성, AddForce와 Velocity 활용
- Maskable을 활용한 PowerBar 구현. interval, max, min을 활용
- Prefabs 사용, Sensors 사용, FloorHit, OnTriggerEnter, OnCollisionEnter 를 이해함
- Instantiate, Destroy를 통해 Object를 생성 및 제거하는 방법을 익힘
- 두개의 Script간 연결 방법을 학습, 그를 통한 다른 요소의 Text를 수정하는 실습을 통해 구현해보며 이해함