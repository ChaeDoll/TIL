# Unity (유니티)  
## 유니티로 AR 정복하기  
### AR Mask 제어 (2023.03.12)  
Unity AR Foundation에도 EyeTracking 기능이 존재하지만,  
전면카메라에 TrueDepth를 지원하는 iOS에서만 지원하는 기능이다.  
즉, ARCore(안드로이드)에서는 Eye Tracking을 사실상 지원하지 않는다.  

안드로이드, iOS에서 공통으로 사용할 수 있는 FaceTracking 기능을 만들어 볼 예정이다.  

기존에 배웠던 AR Default Face 컴포넌트를 보면, 아래에 Material이 지정되어있다.  
이 Material을 바꾸고 터치할 때마다 다른 Object를 얼굴앞에 띄우도록 하는 예제를 해본다.  

코드 내에 GetComponent<컴포넌트명>() 을 사용했다.  
단어에서 유추할 수 있듯, 등록되어 있는 컴포넌트의 내용을 가져와서 코드로 사용할 수 있게 된다.  
switchCount = (switchCount + 1) % materials.Length; 와 같이 배열의 길이만큼 %를 해두면  
0번 인덱스부터 (배열길이-1)번 인덱스까지 순환적으로 돌도록 만들 수 있다.  

ARCore, ARKit의 차이점은 지금 우리가 만든 간단한 어플로도 구분가능하다.  
ARCore는 마스크를 쓰지만 눈 코 입이 전부 막혀있는 형태를 띄고있다.  
하지만 ARKit는 눈 코 입구멍이 다 열려있고 표정변화를 좀 더 잘 인식한다고 생각했다.