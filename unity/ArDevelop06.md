# Unity (유니티)  
## 유니티로 AR 정복하기  
### Eye Tracking with iOS (2023.03.27)  
Eye Tracking 기능은 Android 유저라면 일단 사용하기 어렵다고 봐야한다.  
ARCore를 사용하는 Android에는 FaceTracking에 사용되는 FaceRegion의 구성요소를 3가지 갖는다.  
NoseTip, ForeheadLeft, ForeheadRight 이렇게 세가지이다.  
반면 ARKit을 사용하는 iOS의 경우에는 무려 아홉가지나 가지고있다.  
Left Eye, Right Eye, Mouth, Jaw, Eyebrows, Cheeks, Nose, Tongue, Creating a Blend Shape Location.  
이렇게 사용가능한 구역의 개수부터 다르기 때문에 당연히 트래킹에 있어서 차이가 날 수 밖에 없다.  
강사분도 ARCore로 EyeTracking을 시도해보았지만 안타깝게도 어렵다고 하셨다.  

나는 iOS는 없지만 일단 강의를 보며 iOS를 목표로 하는 개발도 엿보았다.  
Build Setting을 일단 Android가 아닌 iOS로 세팅해야한다.  
또한 ARCore가 아닌 ARKit를 사용하게 체크해준다.  

Scene에서 오브젝트를 생성하여 조정하고 Assets구역으로 가져와 Prefab화 시키는건 유용한듯.  

EyeTracking에서 사용할 때 쓰는 Face 객체는 눈만 인식하면 된다.  
따라서 Default값으로 존재하는 Mesh 구조나 Face Visualizer 컴포넌트들은 삭제해도 된다.  
이후 Session Origin에 AR Face Manager에 Face 인식 Prefab을 등록하고,  
ARCore에서 얼굴을 인식했던 방식처럼 새로운 컴포넌트를 불러와 FaceManager 컴포넌트를 불러온다.  
그리고 void Update메소드에 (매 프레임마다) 얼굴을 인식한 뒤, 그 구성요소인  
Left Eye 혹은 Right Eye에 띄우고자 하는 Object를 객체화 시킨다.  
이전처럼 생성이 되지 않았을 때만 객체화(Instantiate)를 시켜주고,  
이미 생성되어 있다면 transform.position과 rotation으로 위치를 갱신시켜준다.  
