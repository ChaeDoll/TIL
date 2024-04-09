# Unity (유니티)  
## 유니티로 AR 정복하기  
### AR Foundation 기본 설정 (2023.03.08)  
AR Foundation 기능을 사용하면 멀티플랫폼을 사용가능하다.  
기본적으로 안드로이드는 ARCore SDK를 사용하고 iOS는 ARKit SDK를 사용하여 AR앱을 개발한다.  
하지만 Unity의 AR Foundation을 사용하면 이 두가지를 따로 개발할 필요 없이 한번에 개발이 가능하다.  

유니티 프로젝트 내부 창 Window -> Package Manager -> Unity Registry 선택 -> 여러 플러그인을 다운로드 할 수 있다.

만약 Android로 세팅하고싶다면 File -> Build Setting에서 플랫폼 변경 -> Player Setting  
Player Setting에서 AR Foundation이 지원하지 않는 Vulkan을 제거하고,  
Minimum API Level을 24 이상으로 선택한다. AR Foundation에서는 최소 24까지는 되어있어야 동작한다. (안드로이드의 최소 API 레벨)  
이후 패키지명을 바꾸거나 할 때 이 세팅에서 가능하다.  
XR Plug-in 세팅은 Android 빌드가 목적이면 ARCore을 체크한다.  

AR앱을 만들기 위해 필수적으로 필요한 컴포넌트가 존재한다.  
> 우클릭 -> XR -> AR Session 추가 (AR의 전체적인 LifeCycle 관리), AR Session Orgin 추가 (AR요소들을 Unity 공간에 전송하기 위한 컴포넌트), Main Camera 삭제 (이미 AR Session Orgin에 실제 카메라 위치가 내포됨), AR Camera에 Tag를 Main Camera로 설정  

AR Session이 모든 것의 기준점이 되고, 이 내부에 컴포넌트를 추가하면 된다.  

AR Default Point Cloud : 영상에서 얻어지는 특징점들을 노란색 포인트로 표시  
AR Default Plane : 위의 특징점들을 기반으로 평면을 찾는 컴포넌트  
(후면 카메라로 특징점들을 찾고, 그 특징점을 통해 평면을 인식하는 구조)  
Session Orgin에서 컴포넌트 추가하기 기능으로 Point Cloud Manager를 추가 후 연결.  
마찬가지로 또 컴포넌트 추가하여 Plane Manager을 추가 후 연결한다.  

> 갤럭시 USB 연결방법 : 설정 -> 휴대전화 정보 -> 소프트웨어 정보 -> 빌드번호 연타 -> 개발자모드 해금 후 USB 디버깅 켜기  

Build and Run을 했는데 a failure occurred executing... 어쩌구 에러가 떴다.  
알고보니 player setting의 비밀번호 오류라고 한다. 커스텀 비밀번호를 생성하니까 빌드가 성공됐다.  
이후 실행이 안되는 문제가 생겼다. 알고보니 64비트의 기종이 32비트의 어플리케이션을 지원하지 않아서였다.  
Project Setting에서 Configuration부문의 Scripting Backend를 IL2CPP로 변경해주었고,  
Targer Architectures항목의 ARM64를 체크해주었더니 문제가 해결되었다.  

AR Default Face를 추가하면 후면카메라에서 전면카메라로 변경이 된다. 참고하길  
