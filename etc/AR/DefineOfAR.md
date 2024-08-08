<!-- 2023/09/27 작성 -->
# AR의 정의
- 아즈마의 AR정리 (A survey of argumented reality(Ronald Azuma. 1997) 논문 참조)
    - 현실 세계와 가상이 결합된 것.
    - 실시간으로 합성될 것.
    - 3차원 공간에 정합될 것.
- 위 세 가지의 조건을 충족한다면 모두 AR이라고 부를 수 있다.
- 즉, 현실공간에 실시간으로 가상 3D객체가 합성되는 것을 의미한다.

## 필요한 기술
- 어떤 위치에 올려야 할지 (Positioning)
- 객체가 이질감 없이 합성되어야 하고
- 여러 각도에서 바라보았을 때 객체가 변함없이 유지되어야 함
- 각각의 기술 하나하나가 어려운 기술.

## 컨텐츠 개발에 필요한 것
- 잘 만들어져있는 AR엔진을 사용하여 (SDK, Tool etc...) ImageTracking, FaceTracking, PlaneTracking 등 복잡한 알고리즘을 제공
- 개발자는 이렇게 엔진에서 제공되는 정보들을 이용하여 어떠한 컨텐츠를 만들지 고민하기만 하면 된다.
- 구글의 ARCore, 애플의 ARKit, 유니티의 AR Foundation이 모두 AR엔진의 예시들이다.

## 기본 기술
- 위에서 말한 ImageTracking, FaceTracking, PlaneTracking이 기본 기술이다.
- Image Tracking : 현실에서 특정 이미지를 찾아내는 기술
- Face Tracking : 사용자의 얼굴을 추적하여 표정을 인식하는 기술
- Plane Tracking : 현실 공간에서의 수평과 수직을 인식하는 기술
- 이렇게 인식된 세 가지의 Tracking을 토대로 가상의 객체를 현실에 증강시키는 것이다.