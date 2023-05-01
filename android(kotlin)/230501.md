## View와 ViewGroup의 차이  
View와 ViewGroup은 안드로이드 UI요소들이다.  
ViewGroup이 더 상위 객체이고, ViewGroup 내에 여러 View들을 가지고있다.  

View는 TextView, Button처럼 특정 기능을 갖는 컴포넌트이다.  
ViewGroup은 이러한 View들을 내포하는 객체이기에, 내부 View객체들의 UI를 조정하기 위한 객체라고 생각하면 된다.  

ViewGroup은 대표적으로 LinearLayout과 같은 View 객체들을 담는 레이아웃들이 이에 속한다고 생각하면 된다.  
View에는 TextView나, Button처럼 화면에 객체로 비추어지는 위젯들을 말한다.  
