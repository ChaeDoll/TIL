# Unity (유니티)  
## 유니티로 AR 정복하기  
### 얼굴에 오브젝트 올리기 (2023.03.25)  
Session Origin을 통해서 실제 얼굴 위치가 어디에 있는지 받아와야지 AR에서 제대로 맵핑 가능하다.  
ARCoreSubsystem이라는 인터페이스를 사용하여 우리는 GetRegionPoses 메소드를 사용한다.  

어떠한 오브젝트를 올릴것인지 Prefab을 정의해주고,  
그 위치에 실제로 인스턴스화 하여 움직일 게임 오브젝트 선언,  
관련된 기능 수행을 위하여 ARFaceManager, SessionOrigin 가져옴  
FaceRegions에는 ARCore를 통해 얻어진 face의 Region 정보가 들어감  

ARCore의 subsystem을 받아오고 이를 통해 GetRegionPoses를 하여 얼굴에 Region 위치들을 받음  
받아온 정보를 통해 Type을 분류하여 타입별로 object를 배치하는 방식이다.  
기본적으로 Region은 leftHead, rightHead, Nose 세가지로 크게 타입이 존재한다.  
