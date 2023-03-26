# Unity (유니티)  
## 유니티로 AR 정복하기  
### Image Tracking (2023.03.26)  
AR의 대표적인 기능은 주로 세 가지로 분류된다.  
- Plane Tracking  
- Face Tracking  
- Image Tracking  

평면을 인식하여 그 위에 오브젝트를 얹는 것이 Plane Tracking이고,  
얼굴을 인식하여 얼굴 위에 무언가를 얹는 것이 Face Tracking이고,  
이미지를 인식하여 그 이미지 위에 오브젝트를 얹는 것이 Image Tracking 이다.  

그 중에 이번엔 현실의 2D 이미지를 인식하여 가상의 3D 오브젝트를 트래킹하는 실습을 진행한다.  

먼저 XR의 ReferenceImageLibrary를 생성하여 사진을 등록한다.  
이후 AR Tracked Image Manager를 SessionOrigin에 컴포넌트 추가를 해준다.  
거기에 이미지라이브러리를 등록하고, Track할 이미지 Prefab을 등록하기 위해
먼저 필드에 Cube Object를 생성하고, 스크린 화면에 맞게 scale을 조정한뒤 영상을 등록한다.  
이후 영상이 매치된 Object를 Assets으로 끌고오면 Prefab화가 되는데, 이젠 필드에 있는걸 삭제해도 된다.  
이제 ARTrackedImageManager의 트랙할 이미지 Prefab에다 위에서 만든 영상이 매칭된 Object를 등록한다.  

실행한 결과, 등록한 이미지를 화면에 보여주면 그 위치에 등록해둔 영상 Prefab이 실행되는 것을 확인할 수 있었다.  
코드 없이 이와 같은 기능을 구현할 수 있었기에 흥미로웠다.  
다만 내가 등록한 영상이 180도 뒤집혀서 실행되었기에 그것에 대한 이유가 무엇인지 좀 궁금하다.  
