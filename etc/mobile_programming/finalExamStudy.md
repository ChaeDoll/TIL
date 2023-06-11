# 모바일프로그래밍 기말고사 정리  
## 5장  
Fragment()를 상속받아 Fragment로 동작하는 클래스의 경우에는 Fragment에 있는 onCreateView()만을 오버라이딩 할 수 있고 inflater.inflate(R.layout.xxx, container, false) 를 통해 fragment layout을 동적으로 inflates할 수 있다.  

activity_main에서 위젯으로 fragment를 사용할 수도 있다. id는 본인이 원하는대로 지정하고, android:name="com.example.프로젝트명.클래스명" 과 같은 형식으로 위에서 만든 Fragment 클래스를 위젯으로 연결할 수 있다. 반드시 Package명을 써주어야 한다.  

Activity내에서 동적으로 Fragment를 추가(변경)해줄 수도 있다.  
위젯을 포함하는 Fragment를 만들고, 위에서 설정한 것 처럼 onCreateView와 inflater를 통해 호출되면 fragmentLayout이 호출되도록 설정해둔다.  

FrameLayout에 Fragment를 부르고, replaceFragment 메소드를 통해 다른 Fragment로 교체한다.  
replaceFragment는 우리가 만든 메소드...  
> fun replaceFragment(fragment : Fragment)메소드  
val fragmentManager = supportFragmentManager를 사용하여 불러오고,  
val transaction = fragmentManager.beginTransaction()을 사용하여 변환모드를 사용한다.  
transaction.replace(R.id.rightLayout, fragment)  
transaction.commit() 을 사용하여 변환한다.  

Fragment의 Back Stack을 이용하여 변경하기 이전 fragment상태로 돌아가는 방법도 있다.  
FragmentTransaction이 갖고있는 addToBackStack()메소드를 통해 변경하기 이전상태를 stack에 저장하게 할 수 있다.  

