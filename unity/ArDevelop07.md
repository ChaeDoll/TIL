# Unity (유니티)  
## 유니티로 AR 정복하기  
### 중간점검 프로젝트 세팅 (2023.03.27)  
AR프로젝트를 위해서 우리가 Unity 환경에서 추가해줘야 할 것들을 정리한 내용이다.  
- 먼저 프로젝트를 생성하며 시작한다.  
- Package Manager 메뉴를 통해 Unity Registry를 다운로드 받아줘야한다.  

우리는 AR환경을 사용하기 위해 AR Foundation과, ARCore(Android) 그리고 ARKit(iOS)를 받아주어야 한다.  
다 설치가 완료되면 Scene 탭에 우클릭을 하여 XR탭이 새롭게 생긴것을 확인할 수 있다.  
- XR 탭에 있는 AR Session과 AR Session Origin을 생성해준다. (필수)  

AR Session은 AR 구축을 위한 주요 프로세스들을 관리하는 객체이다.  
카메라를 통한 이미지 데이터나 모션 데이터들을 받아와 이미지 분석, 알고리즘 수행하는 역할을 한다.  
이에 대한 결과를 바탕으로 실제 현실세계와 가상세계의 연결을 구축해준다.  
간단하게 요약하면 AR 전체적인 생명주기를 관리하는 객체라고 보면 된다.  

AR Session Origin의 경우에는 가상공간에서 렌더링 된 AR 컨텐츠들을 현실 좌표 공간에 매핑하기 위한 객체이다.  
AR 객체들의 scale을 조정하거나 오프셋을 적용.  
기본적으로 AR카메라를 갖고있고, 이것이 사용자 디바이스의 카메라의 위치로 설정된다.  
AR Camera 객체의 속성을 보면 AR Camera Manager 부분에 Facing Direction이 존재한다.  
이것이 World이면 후면카메라, User이면 전면카메라를 의미한다.  
본인의 프로젝트에 맞게 설정해주면 된다.  
여기에 있는 AR Camera가 우리가 사용한 기본카메라이기에 프로젝트 생성 시에 자동으로 존재하는 Main Camera 오브젝트는 삭제를 해줘도 된다.  
이후 AR Camera의 Tag를 Main Camera로 세팅해준다.  

Assets에 존재하는 Scene폴더 내부에서 Scene의 이름을 변경할 수 있다.  
하나 앱에서 여러 기능들을 다 수행할 수 있도록 Scene을 나누어 개발한다.  
> 예를 들어 A씬에서 전면카메라를 사용하는 기능, B씬에서 후면카메라를 사용하는 기능  

여기까지 잘 따라온다면 앱을 실행하면 기본적으로 카메라가 실행되는 어플리케이션이 완료될 것이다.  

빌드는 Build Setting에서 빌드 할 Scene을 선택하고, 원하는 플랫폼으로 Switch해준다.  
Android의 경우에 먼저 USB를 통해 디바이스를 컴퓨터에 연결해준다.  
Player Setting을 통해 회사명, 제품명, 아이콘 등을 등록할 수 있다.  
일단 중요한 설정부터 보면,  
> Graphics API에서 기본적으로 Vulkan이 포함되어 있다.  
현재 AR에서는 이것이 지원되지 않기에 따라서 이를 지워준다.  
Minimum API Level도 24로 설정해준다.  
64비트 환경에서 앱이 실행되지 않는 오류를 해결해주기 위한 설정도 필요하다.  
Configuration탭에 Scripting Backend를 IL2CPP로 설정하고 하위에 Target Architectures에 ARM64를 체크해준다.  
마지막으로 XR Plug-in Management에 ARCore를 활성화 시켜주면 된다.  
필요에 따라서는 Publishing 설정에 Key를 세팅해야할 수도 있다.  

앱 설정을 마쳤다면 앱을 빌딩해준다.  
