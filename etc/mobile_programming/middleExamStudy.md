# 모바일프로그래밍 중간고사 정리  
## 1장  
### 안드로이드 역사  
2003년 앤드 루빈(Andy Rubin)이 안드로이드(Android) 설립.  
2005년 구글이 안드로이드 인수. 앤드 루빈이 프로젝트를 그대로 담당  
2008년에 안드로이드OS 첫번째 버전 출시. 리눅스 기반으로 하는데 2010년에 리눅스 팀에 의해 리눅스 커널 메인 브랜치에서 제거. 초창기엔 모든 앱 자바로 개발  
오라클도 구글을 정보침해로 고소 -> 구글이 패소  
구글은 안드로이드를 개방형 OS로 만들었음  
### 안드로이드 시스템 구조
안드로이드의 계층은 4개  
- 리눅스 커널 계층 : 다양한 하드웨어용 드라이버  
- 시스템 라이브러리 계층 : 개발을 위한핵심 라이브러리 제공  
- 애플리케이션 프레임워크 계층 : 앱 빌드에 사용하는 모든 종류의 API  
- 애플리케이션 계층 : 모든 앱이 속한 계층  

버전 5.0에서 ART 사용으로 Dalvik 가상머신을 대체하여 앱 속도 크게향상  
### 안드로이드 시스템 특징  
- Activity : 앱 UI 표시에 사용. 사용자가 볼 수 있는 모든것이 Activity에서...  
- Service : 보이지 않지만 앱 종료해도 백그라운드 실행 가능  
- BroadcastReceiver : 앱으로부터 broadcast 메세지를 수신하거나 보낼수있음  
- ContentProvider : 서로 다른 앱 간 데이터를 공유할 수 있다. 대신 사용자가 시스템에서 접근할 권한을 줘야한다?  

위 네 가지 주요 구성 요소와 함께  
풍부한 시스템 위젯이 제공되고,  
가볍고빠른 관계형데이터베이스 SQLite를 사용  
강력한 멀티미디어 지원 : 음악, 동영상, 음성녹음, 사진촬영 같은...  

### 프로젝트 생성..  
앱 : 모든 코드나 리소스파일은 이 폴더 아래에 있음.  
gradle : 기본적으로 안드로이드 스튜디오는 gradle로 라이브러리를 받아옴..??  
등등... 여러가지 있는데 앱 폴더 외에는 대부분 폴더나 파일은 자동생성되어 수정할 필요 없다.  

앱 폴더 - build, libs, src 등 여러개 있음  
src 내에는 test폴더와 main폴더, main내에는 java나kotlin 코드가저장되는 java폴더, 이미지나 레이아웃 문자열 등 프로젝트에 쓰이는 모든 리소스가 담겨있는 res폴더가 있음.  
전체 안드로이드 프로젝트 구성 파일로 AndroidManifest.xml파일도 main폴더 내에 있음  

AndroidManifest에서 intent-filter 코드에서 앱 아이콘을 클릭할때 실행되는 Activity를 설정가능?  

### 기본 코드들  
MainActivity는 AppCompatActivity 상속한다.  
Activity 클래스는 안드로이드 시스템의 기본클래스. 앱에 정의된 모든 Activity는 이 클래스나 하위 클래스를 상속해야 Activity의 기능이나 속성 이용 가능.  

Activity가 생성될 때 onCreate() 메소드가 호출됨.  onCreate()안에서 setContentView()가 호출되는데, 이 안에서 activity_main 레이아웃을 가져온다.  
따라서 activity_main.xml에 TextView 위젯을 사용하여 텍스트를 표기하면, 화면에 이게 나온다.  

### 리소스  
이미지는 drawable 폴더에 저장.  
앱 아이콘은 mipmap 폴더 사용  
문자열, 색상 등은 values 폴더 사용  
레이아웃은 layout 폴더 사용  
안드로이드 스튜디오에서는 drawable-hdpi나 xhdpi, xxhdpi 등 폴더를 직접 생성해야한다.  
> 앱 개발시엔 동일한 이미지를 다양한 해상도로 폴더에 넣는것이 좋음. 현재 디바이스에 맞는 리소스가 선택됨  

리소스 참조를 가져오는 방법은 크게 두가지이다.  
만약 values/string.xml 파일을 참조하고 싶다면,
우선 string.xml파일을 보면  
<리소스> <스트링 name="app_name">프로젝트이름</....    
이런식으로 되어있다면  
R.string.app_name을 사용하거나  
xml 파일에서 @string/app_name을 사용하는 것이 방법이다.  

### Gradle  
Gradle은 프로젝트 빌드를 위한 고급도구. Groovy 기반 DSL을 사용하여 ...  

### 로깅 
Log 클래스를 사용하면 콘솔에 로그 출력 가능 
Log메소드엔 v(), d(), i(), w(), e()같은것이 있는데, 보통 우린 Log.d() 사용하는듯  
Log.d("태그", "msg") 일반적으로 첫번째로 현재 클래스명을 쓰고 두번째엔 인쇄할 콘텐츠를 쓴다.  
logcat을 통해 확인 가능  
프로젝트 규모가 클수록 디버깅을 위한 정보출력 도구로 print()보다는 Log가 더 유용하다.  
필터 기능을 통해 선택한 애플리케이션만 표시할 수도 있고...  
logcat으로 수천줄 로그 중, 오류 로그만 표시할 수도 있다.  

## 2장  
### 코틀린!  
2019년 구글은 코틀린을 안드로이드 애플리케이션 권장 언어로 선택하였다.  
향후 공식 API도 주로 코틀린으로 제공될 것임  
GooglePlay스토어 상위 앱들 중 60%가 Kotlin으로 개발. 매년 증가 중  

<b>Kotlin은 JetBrains에서 설계 및 구현</b>  
2011년초에 첫번째 버전 발표하고 2012년에 오픈소스로 공개  
2016년에 버전 1.0발표됨. (충분히 안정화 됨)  
2017년에 구글은 Kotlin이 안드로이드 개발을 위한 우선수위가 되어야한다 발표함  

프로그래밍 언어는 크게 compiled언어와  interpreted언어로 나뉜다.  
compiled언어는 컴파일러가 컴퓨터가 즉시 사용가능한 이진파일로 한번에 소스코드를 컴파일하는 언어이다. C나 C++이 여기에 속함   
Runtime속도가 빠른 대신 견고하게 써야한다.  

imterpreted언어는 다르다. 스크립트 언어라고도 불리고 한줄 한줄 기계어로 번역해서 속도가 느리지만 융통성이 있다. 파이썬, 자바스크립트가 여기에 속한다.  

자바(Java)는 실행하기 전 컴파일이 필요하지만, 컴파일 된 코드가 이진코드로 변환되는 것이 아닌, JVM(자바 가상 머신; 모바일은 ART)에서 이해하는 특수 클래스파일로 컴파일 된다. 이 가상머신이 interpreter 역할을 하여 이 특수 클래스파일을 이진법으로 해석하여 클래스가 실행될 수 있도록 하기에, <b>Interpreted언어</b>라고 할 수 있다.  
JVM은 자바코드가 아니라 컴파일된 클래스 파일에 작용하는것이고...  

따라서, 새로운 언어를 만들어 개발하고 컴파일러를 통해 JVM이 인식하는 형식에 맞는 파일로 컴파일된다면 Java 언어가 아니더라도 동작이 가능할 것이다! ==> 이것이 Kotlin(코틀린) 작동 원리  
이 덕에 JetBrains는 타사지만 Android 앱 개발을 위한 언어 설계 가능  

### 왜 코틀린이 자바에 비해 우수한가?  
- 동일한 기능에서 Kotlin이 Java보다 설치공간 50%이하  
- Java에 비해 Kotlin은 개발 효율성을 크게 향상시키는 많은 SyntaxSugar를 갖는다.  
- Kotlin은 언어 안전에 많이 주의를 기울인다. NullPointerException을 거의 제거 가능하다  
- 자바와 100%호환된다. Java코드를 직접 호출하고, 타사 API나 프레임워크 원활히 사용가능  
- 자바 몰라도 Kotlin을 배울수는 있지만 Java에 대한 이해가 높은 개발자에 비해 개념이해가 어려울 수 있다.  

### 코틀린 기본 문법  
<b>출력</b>은 print()혹은 println()으로 가능  
main 함수 형태는 fun main(){}  

<b>변수</b> : Java에서는 변수 유형을 int a, String b 처럼 유형지정이 필수적이다.  
Kotlin은 변수 선언시 val과 var만 존재한다.  
val은 Java의 final 키워드와 같고, var은 일반 변수들을 의미한다.  

<b>문법</b> - Java는 문장 끝마다 세미콜론을 사용한다.  
하지만 Kotlin은 세미콜론이 필요없다.  
기본적으로 Kotlin은 Type을 자동으로 추측하지만, 원하는 Type을 미리 지정하고 싶다면 다음과 같은 구문을 사용한다.  
val a: Int = 10  
콜론(':')을 사용하여 변수의 type을 지정해두면 지정하여 타입을 사용할 수 있다.  
이렇게 설정한 경우에는 다른 type의 값이 들어올때 Exception을 발생된다.  

(중요) Java에서는 type명을 소문자로도 적었을텐데..  
Kotlin에서는 int, char 등 원시type을 모두 제거했다.  
따라서 Kotlin은 Int, Char, Long, Short, Float, Double, Boolean, Byte와 같이 대문자로 type을 정해두었다.  
그리고 이들의 데이터타입은 Java에서 Integer 등등 처럼 메소드를 갖는 객체 유형들로 존재한다.  

만약 val을 재정의하려하면 오류가 난다.  
java에서 final을 재정의 할 수 없는것과 동일  
var을 쓰면 변경가능함  

사실 Java에서도 final을 사용한 코딩을 더욱 권고하는 바이다. 하지만 실제로 많은 개발자가 그런 습관을 갖고있지 않다.  
Kotlin은 아예 val, var로 구분하여 final 키워드를 더욱 접근성이 좋게 하였음  
모든 변수에 final이 붙는게 원래 좋은코드!  

### 기능  
함수 선언은  
fun 메소드명(파라미터이름: 타입, 파라미터이름2: 타입): 리턴타입 {return ...}  
이런 형태로 이루어져야 한다.  

만약  
fun largerNumber(num1: Int, num2: Int): Int{  
    return max(num1, num2)  
}  
이런 방식으로 식을 작성하면  
매개변수로 2개의 숫자를 받아서 max(a, b)한 결과를 정수형 타입으로 반환한다.  

### Syntax Sugar 문법축약  
너무 많은데... 차근차근 정리해보면  

1. 한줄코드는 '=' 등호를 쓰면 {}중괄호 생략 가능.  
등호만으로 return 키워드도 생략 가능하다는점!  

어느 함수 내부에
val value = 0  
if (num1>num2){value=num1} else {value=num2}  
return value  
이런 문법이 있다면,    
val value=if(num>num2)  이것처럼 if문을 직접 넣은뒤 return해도 되고  
아예 val선언 안하고 return if(num...)처럼 해도 되고  
한줄만 있는 코드 상 중괄호를 생략하고  
1번에서 말한 것처럼 return 대신 등호를 넣어  
fun .... = if (num1>num2) num1 else num2  
이렇게 할 수 있다.  
진짜 많이 간소화된 모습!  

### Syntax Sugar when문법  
Kotlin의 when은 Java의 switch라고 생각  
if else if...반복은 때로는 너무 많아보임  
when(조건) {조건값1 -> 반환값  
조건값2 -> 반환값2  
else -> 반환값n  
}  
이런 표현도 가능하다.  
물론 여기서도 1번 규칙처럼 한줄이면 중괄호{}생략 가능하다.  
데이터(값)일치 확인도 가능하지만,  
타입(유형)일치 확인도 가능하다.  
is Int 처럼...  

번외.. Java에서 equals() 쓰듯이 Kotlin에서 '=='를 사용가능.  
인수를 name에 받고 name.startsWith(값)을 when내부에 넣어서 값으로 시작하면 전부 특정문장을 만족하도록 할수도있음  

### Syntax suger 루프문  
반복문은 Java와 Kotlin이 유사하다. while, for루프 다 있고 while은 Java와 동일  
Kotlin은 for문이 다르다  
val range = 0..10으로 범위를 포함시킬수있는데 [0,10],  
for (i in 0..10) 처럼 0~10까지 사용 가능하다.  

우리가 아는 0,10 (0부터 9까지 사용)을 하려면?  
val range = 0 until 10 을 사용하면 [0,10)의 범위를 가진다.
for in 루프는 반복때마다 기본적으로 +1을 한다.  
단계적 이동을 위해 until을 사용할 수도 있다.  
for (i in 0 until 10 step 2)를 사용하면  
Java에서의 for(i=0; i<10; i+=2)와 같다.  
내림차순으로 for(i in 10 downTo 1)도 있다.  
이 경우 [10,1]의 범위로 간다.  
for in루프는 배열이나 집합에 적용도 가능  

### 객체 지향 프로그래밍  
OOP(Object-Oriented Programming)은 클래스 생성가능해서 C같은 구조적 프로그래밍과 다름  
클래스는 추상화하여...  
클래스는 필드, 메소드를 가질수있고 필드는 속성, 메소드는 클래스의 동작을 의미한다.  
필드와 메소드를 캡슐화하여 객체 만들고 그 필드와 메소드 활용해서 프로그래밍 가능.  
이런 개념외에도 상속, 다형성 등 다른 기능도...  

### class 생성  
Java처럼 클래스 생성  
class 클래스명 {  
    속성  
    메소드(){...}  
}  
이렇게 만든 클래스를 다른 곳에서 사용가능  
fun main(){  
    val p = 클래스명()  
    p.속성="속성값"  
    p.메소드()  
}  
이런식으로 사용가능  

### 상속  
Java와는 달리 Kotlin에서는 상속을 남용하지 않기위해 아무 클래스나 상속할 수 없다.  
따라서 추상클래스가 아닌 모든 클래스는 기본적으로 상속이 불가능하다.  
<b>open</b> 키워드를 추가하면 상속이 가능해진다.  
open class 클래스명 {...}  

이렇게 상속이 가능해진 상태가 되었다면, 이제는 상속할 클래스에도 상속한다는 문법을 추가해주어야 한다.  

class 자식 : 부모() {...}  
이런 방식으로 open으로 상속가능 상태인 부모클래스를 상속받을 수 있다.  
> Java에서는 상속시에 부모클래스 뒤에 괄호가 없는데..? -> Kotlin은 기본생성자, 보조생성자같은 고급 개념을 위해...  

### 생성자  
위에서 생성자 이야기를 했다.  
기본 생성자는 메소드에 쓸 필요가 없고, 물론 필요시 안에 명시할 수도 있다.  
클래스 이름 바로 뒤에 매개변수 바로 넣을수있음.  

class 자식(val a:String, val b:Int):부모() ..  
이런방식으로말이다.  
이제 자식객체를 만들기 위해선 자식("a", 2)처럼 값을 매개변수값을 함께 넣어줘야함  

클래스 내부에 init을 통해 생성 시에 바로 실행되는 메소드를 만들 수도 있다.  
자식클래스가 부모클래스를 상속받을때 부모클래스에 괄호가 있는 이유는 부모의 생성자 호출을 위해서다.  
괄호 비어있다는건 매개변수없는 부모 생성자 호출한다는 것.  
<b>매개변수 없어도 괄호 생략못한다.</b>  

만약 부모클래스가 생성을위한 매개변수가 있다?  
그러면 자식에서 상속받을때 이 매개변수값도 넣어줘야한다. 안그러면 오류나옴  

만약 매개변수를 갖는게 기본값이지만 매개변수값 안넣어도 생성되도록(오류없게) 하고싶다? 그러면 안에 constructor라는 보조생성자를 통해 지정가능함.  

class Student(val sno: String, val grade: Int, name: String, age: Int): Person(name, age) {  
 constructor(name: String, age: Int) : this ("", 0, name, age) {  
 }  
 constructor() : this("", 0) {  
 }  
}  
복잡하네..  

하지만! super()를 사용하여 부모생성자 직접호출 가능  

### 인터페이스  
자바와 매우 유사  
그냥 interface 이름 {  
    fun 메소드명()  
}  
이렇게 두고  
상속시에 클래스 상속처럼 콜론(':')뒤에 쓰면 됨. 여러개면 ','사용  

자바는 상속을위해 extends를 쓰고 구현을위해 implements를 쓰는데 Kotlin은 :이랑 ,만 필요  

인터페이스를 받았으면 그것에 대한 구현 메소드를 오버라이딩하여 재정의해야한다.  

인터페이스로 다형성, 인터페이스지향프로그래밍이 가능해짐  
Kotlin에서 interface지만 메소드에 구현을 해놓을 수 있다. 자바에서 default와 동일하다보면 된다.  
이러면 재정의안해도 문제없음. 인터페이스에서 구현된 메소드가 출력될 것이다.  

### 메소드 범위유형  
Java에서 public, private, protected, (default)이렇게 4가지가 있었을 것이다.  
Kotlin은 public, private, protected, internal 이렇게 4가지가 있다.  
fun 앞에 붙여서 지정이 가능하다.  

private는 둘다 똑같이 작동하고  
Kotlin에서는 기본값이 public이다.  

Java에서 protected는 현재클래스 ,하위클래스, 동일 패키지에 있는 클래스에 접근가능을 의미  
Kotlin은 현재클래스, 하위클래스만 보호  

Kotlin은 default 대신 internal을 사용  
모듈 내에서만 작동하도록 범위설정 가능하다.  

### 데이터클래스 (data class)  
원래는 데이터에 관한 클래스 생성하면 equals(), hashCode(), toString()을 재정의해야함  
근데 Kotlin에서는 data 키워드만 class앞에 붙이면 자동으로 위 애들을 알아서 구현해줌  

Java에서는 Singleton 구현하기 위해서  
클래스 내부에 static으로 Singleton instance를 선언하고, 본인 클래스를 호출하여 싱글톤을 구현한다.  
그외에도 싱글톤 구현방법은 다양한데...  
getInstance()메소드를 만들고 호출하는방법도 있고...  

Kotlin에서는 싱글톤 구현은 간단하다.  
object 싱글톤클래스명 {}  
이것만으로 전역에서 사용가능한 싱글톤 객체가 선언된다.  
static한 성질을 갖고있기에 object 내부에 선언한 여러 메소드는 싱글톤클래스명.메소드명()으로 접근가능하다.  

### 람다표현식  
람다표현식은 최신고급프로그래밍언어에서 지원받음  
Java는  JDK1.8부터 지원함(늦게) 그래서 람다 표현식 사용 안하는 프로그램이 많음  
Kotlin의 강력한 기능중 하나가 바로 람다표현식이다.  

람다표현식 사용하는 완벽한예시 --> 컬렉션  
List, Set, Map들은 Java의 인터페이스  
집합은 HashSet, 맵은 HashMap을 가장많이씀  

우리가 만약  
val list = ArrayList<String>()을 선언하고  
list.add("Apple")
list.add.... 이렇게 여러가지를 추가한다치자  

하지만 코틀린으로 간단하게  
val list = listOf("Apple", "Bana....") 쓸 수 있다.  
listOf는 변경불가능한 컬렉션이다. 읽기전용  
변경불가니까 val과 같이사용하기 좋음  
변경 가능한 mutableListOf()도 있긴하다.  

이전에 for문 쓴거 기억나는가  
for (fruit in list) print(fruit)로  
val list 내부의 값들을 순환하여 출력가능하다.  

listOf처럼 setOf(), mutableSetOf() 사용가능  
근데 Map은 val map = HashMap<String, Int>()  
map.put("Apple", 1)...  
이렇게 자바처럼도 쓸수있지만,  
이걸 한번 최적화하면  
val map = HashMap<String, Int>()  
map["Apple"]=1  
....  
이렇게할 수 있고, 이는 곧 mapOf()나 mut..MapOf()를 써서  
val map = mapOf("Apple" to 1, ...) 이렇게 사용가능하다  

map은 for문 출력하려면 이렇게한다  
for((fruit, number) in map) println(fruit+number)  

### 람다 - 컬렉션의 함수형API  
함수형API로 여러가지를 간소화 할 수 있다.  
최대 길이를 갖는 과일을 찾기위해 변수를 선언하고 반복문으로 가장 큰 길이를 갖는지 전부 비교하여 가장 큰 길이를 찾는 식이...  
list.maxBy{it.length} 같은 형태로 바로 뽑힌다.  

그래서 람다가 뭔데?  
람다란 인자로 사용할수있는 몇줄의 코드이다.  
기존엔 데이터를 인자로만 전달했는데, 람다 사용하면 몇줄의 코드를 인자로 전달가능  

람다표현식 구문은 다음과 같다.  
{param name 1:param type, param name 2:param type -> function body}  

이 예시로 val lamda = {fruit:String -> fruit.length}를 사용하면,  
문자열 인자를 받아 length를 반환하는 람다식으로 만들고,  
이 람다식을 인수값으로 list.maxBy(lamda)를 쓰면 list내에서 문자열의 값들이 length형태로 바뀌어 최대값이 반환될것이다.  

최적화하여 위에서 lamda를 선언 안해도 된다.  
바로 val maxLength = list.maxBy({람다식})  
그리고 람다표현식이 함수의 마지막 매개변수라면  
함수 괄호 밖으로 나갈수있음  
val maxLength = list.maxBy(){람다식}  
또한 람다표현식이 유일 매개변수면 () 없애기가능  
유형추론 기능으로 사실 String밖에 없는 list면 타입 안적어도되니까 {fruit->fruit.length}로 간소화 가능  
마지막으로 람다표현식에 매개변수가 하나만있으면 'it' 키워드로 간소화가능  
val maxLength = list.maxBy {it.length} 이렇게 완성  

필터라는 기능도 있다  
list.filter {it.length<=5}.map{it.toUpperCase()} 하면 길이 5이하만 upper됨  
필터먼저걸고 map도 가능  

any라는 키워드와 all이라는 키워드도 있다.  
list.any{람다식} 는 람다식을 리스트내에 하나라도 람다식을 만족하는값이 있는지,  
list.all은 모두만족하는지 Boolean으로 반환하는 애들이다.  

### 함수형API의 활용? Java메소드 호출 
Kotlin에서 Java메소드가 하나의 메소드만 갖는 인터페이스라면 Kotlin에서도 사용이 가능하다.  
만약 인터페이스에 메소드 여러개면 함수형인터페이스가 아니다.  

오직 하나!의 메소드만 가질때  
public interface Runnable {} 와 같은 자바 메소드를 사용가능하다.  
보통 thread에서 사용하나보다.  

익명클래스를 사용하는 원리?  
Thread(object:Runnable{  
    override fun run() {  
        println("Thread is running")  
    }  
}).start()  로 thread 사용.  
하나 메소드 실행... 근데 이거 간단히 가능  
Thread(Runnable{  
    print("Thread")  
}).start()  로도 가능 애초에 메소드 하나고, Runnable도 하나니까...  

Kotlin은 Runnable뒤 람다표현식에서 run() 메소드 구현가능하다.  
사실 인터페이스 메소드 하나있으면 인터페이스명도 생략가능하다.  
Thread({  
    print("Th")
}).start()  
람다식이 마지막 매개변수고... 유일한 매개변수라 괄호생략 다 하면...  
Thread{print("Th")}.start()  

### Null에 안전  
nullable타입덕분에 안정한편이다. null이 나올수있음을 명시하여 nullpointexception피함  
타입?을 쓰면 아래에 null이 아닐때에 반응을 추가해야함 예를들면 if(a!=null) a.do()  
근데 아예 a?.do() 이렇게 두면 자동으로 null이 아닐때 실행하는 구문으로 사용됨  

그러면 null이 아닐때, null일때 둘이 서로다른 메소드를 실행시키고 싶다면?  
val c = a ?: b 를 사용  
null이 아니면 a, null이면 b 실행  
?와?:를 같이사용도 가능  
text?.length?:0 하면  
text가 null이면 text?.length는 ?:에 의해 0을 반환  
값이 있다면 text?.length에 의해 길이 반환  

null이 아니라고 확신하는 기호는 바로 '!!'이다.  
컴파일을 위해 null이 아니라고 보장해주는 것이다.  

람다표현식... 매개변수 하나만있으면 매개변수 이름 필요없어..  

### 문자열 추가  
지금까지 문자열을 잇기위해 +연산자로 이어나감  
하지만 Kotlin은 그럴 필요가 없다!  
"hi, i'm ${obj.name}. nice to meet you"로  
바로 값을 가져올 수 있다.  
변수가 하나면 중괄호생략하여 $name도 가능  

### 메소드 기본파라미터  
파라미터로 num:Int, str:String 이런건 해봤지만 이것도 된다.  
str:String="hello") ..  
기본값을 할당하여 호출시에 바로 기본값 도출할 것이다.  
이렇게 지정해버린 경우에는, 파라미터로 num에 관한 인자만 넣으면 된다. 만약 메소드(123, "hi")를 해도 123만 인자로 사용되고 hi는 무시될것이다.  

첫번째 파라미터를 기본값설정 해버리면?  
메소드("hi") 하면 타입잘못넣었다고 오류  
하지만 메소드(str="hi")를 하면 위치상관 문제없다!  
인수일치를 위한 파라미터명 사용이다.  

보조생성자가 필요없는 이유?  
그냥 생성시에  
class 클래스명(val a:String="", val b:Int=0) {}  
이렇게 해버리면 그냥 클래스명() 처럼 인자값없이 그냥 선언해도 기본인자가 들어가서 문제없다! 물론 인자 넣으면 넣는대로 괜춘


## 3장  
### 안드로이드 스튜디오  
모든 Activity에서 onCreate()를 재정의 해야한다.  
그래서 Activity 생성하면 기본적으로  
override fun onCreate(saved.....) {  
    super.onCreate(saved....)  
}  
onCreate()메소드가 자동으로 만들어진다.  

화면에 무언가 띄우기 위해 우리는 layout을 필요로한다.  

Design모드에서는 어떻게 화면이 보이는지 볼 수 있고, TextMode에서는 xml파일로 레이아웃을 편집할 수 있다.  

layout에서는 orientation 속성이  
horizontal 이냐 vertical이냐에 따라 위젯들의 나열 방향이 결정된다.  
horizontal은 기본값(default)로 가로배치이다.(좌에서 우로)  
vertical로 설정하면 위젯이 세로로 나열된다. (위에서 아래로)  

id 속성은 위젯의 고유ID를 부여하는것이다.  
@+id/id_name을 사용하여 다른 xml 파일에서 이 id_name을 갖는 위젯을 참조할 수 있다.  

match_parent는 레이아웃 크기에 맞춘다.  
wrap_content는 콘텐츠의 크기에 맞게 변하는 사이즈이다.  
버튼같은 콘텐츠는 Text 속성으로 내부에 Text를 넣을 수 있다.  

이렇게 layout을 만들었다면 onCreate()된 Activity를 화면에 보여줘야한다.  
setContentView(R.layout.레이아웃명)을 사용하여 레이아웃의 컨텐츠들을 화면에 띄워준다. R을 사용하여 레이아웃 주소의 id를 가져올 수 있다. 여기의 id는 위에서 설정한것  

### AndroidManifest  
이 파일에서는 앱의 이름을 설정하거나 초기 intent-filter태그를 사용하여 Activity를 설정하거나 할 수 있다.  
intent-filter를 사용하면 android:exported를 true로 해야한다  
이 속성은 다른 앱에서 Activity에 접근할 수 있는지 없는지를 나타내는데, 홈화면 혹은 다른앱에서 런쳐로 설정한 Activity를 실행하려는데 접근못하면 못열겠지?  
false로 하면 같은 앱 내에서 이동은 가능  

### 버튼 활용  
레이아웃에 등록된 기능 중, 버튼같이 상호작용이 필요한 경우 변수를 선언하여 동작을 넣을 수 있다.  
그를 위해 findViewById(R.id.레이아웃id)가 필요하기도 하고  
버튼의 경우 동작을 위해 먼저 버튼을 선언하여 findViewById를 해준뒤,  
Button 객체 메소드인 setOnClickListener를 사용하여 버튼을 눌렀을 때 onClick()메소드가 동작하는 메소드를 만들 수 있다.  
따라서 동작할 메소드는 onClick()에 기입하면 되는데... 보통 람다식으로 넣는듯..?  
+추가 : Activity에 View.OnClickListener 넣으니까 onClick메소드 재정의해줘야함  
그리고 여기에 적은 메소드들이 setOnClickListener에 반응하여 실행됨.

### 토스트메세지
Toast.makeText()로 메세지를 만들고 .show()로 화면에 토스트메세지를 띄울수있음  
makeText메소드는 context, "message", message_time 이렇게 3개의 인자를 필요로한다.  

### 메뉴  
앱을 보면 menu기능이 있는데, res파일에 menu폴더를 만들고 그 안에 main.xml을 만든뒤 menu태그와 함께 item들을 추가하여 메뉴들을 만든다.  
Activity에서 onCreateOptionMenu()를 오버라이드하여 menuInflater.inflate로 불러와주면 된다.  

### inflate  
Inflater 객체들은 inflate()메소드를 사용할 수 있다. 인스턴스를 가져와 생성하는 기능인데,  
menu inflate에선 2개의 매개변수를 사용한다.  
리소스파일(R.menu.main), onCreateOpt...()메소드 인자로 들어온 메뉴 인수  
마지막으로 값을 true로 반환하면 메뉴가 표시되고 false하면 메뉴가 안보인다.  

메뉴 표시가 되었으면 기능도 추가해야 한다.  
onOptionItemSelected 메소드를 오버라이드하여 위에서 들어온 메뉴아이템을 받아 when함수 같은걸 사용하여 id를 확인하고 메소드를 실행시키는 등 여러 활용 가능하다.  
얘도 마찬가지로 return값으로 표시/비표시를 나타낸다.  

### Activity 삭제  
Activity는 기본적으로 뒤로가기하면 현재Activity가 지워질것이다.  
근데 뒤로가기버튼을 안써도 finish()메소드를 사용하면 Activity를 종료할 수 있다.  

### Activity 간 상호작용  
Intent를 사용하면 다른 Activity들 끼리 상호작용이 가능하다.  
Intent를 사용하여 Activity를 시작하거나 Service를 시작하거나 Broadcast를 시작하는 등 가능  

명시적, 암시적 Intent 두 유형이 있다.  
명시적인 경우엔  
Intent(패키지context, class명)으로 호출가능  
예를들어 val intent = Intent(this, SecondActivity::class.java)를 하고,  
startActivity(intent)를 사용하여 Activity를 시작하면  
intent 변수에 저장된 SecondActivity가 시작한다.  

이렇게 명시적으로 나타낸경우 말고, 암시적으로 나타낸다면 AndroidManifest를 사용하여 가능하다.  
intent-filter를 걸고 action태그에 임의로 name을 지정하고 category name도 지정한뒤,  
val intent = Intent("com.example....actionname")을 Intent처럼 사용하고 startActivity(intent)로 시작  

category를 DEFAULT로 설정되있는건 startActivity()가 실행될때 즉시 intent instance로 추가됨  
각 Intent는 하나의 action만 할 수 있지만 category는 여러개 가질수있음.  
addCategory("카테고리명")으로 Menifest에 있는 또다른 카테고리를 가져올 수 있다.  

### 암시적 Intent ...  
암시적Intent 사용하면 앱 내부 아니여도 다른앱 활동도 사용 가능하다.  
웹 표시도 val intent = Intent(Intent.ACTION_VIEW) 하고  
intent.data = Uri.parse("주소") 한뒤 Activity를 start하면 가능.  
uri = {url, urn} 을 의미  

버튼을 눌러 웹 사이트로 연결하기 위한 방법도 있다.  
새 Activity에서 intent-filter로 tools:ignore="AppLinkUrlError"을 속성에 넣고  
그 안에 action은 android.intent.action.VIEW 그리고 data태그로 scheme="https"를 해주면 된다.  

### Activity 데이터 전달  
putExtra 기능으로 ("변수명", data) data를 intent에 넣고 다른 activity에 옮길수있다.  

전달한 것을 가져오기위해 다른 Activity에서는  
val 변수명2 = intent.get타입Extra("변수명")처럼 사용가능  

### 마지막 Activity로 Data 돌려보내기  
startActivityForResult(Intent, requestCode) 메소드 사용하여 이전 활동으로 복귀  
원리는 putExtra로 데이터를 setResult()해서 intent를 반환하고  
이전 Activity에서 onActivityResult 메소드를 오버라이딩하여 intent를 반환받는다.  

우리가 뒤로가기 버튼을 눌렀을때 실행되는것도 오버라이딩 가능하다. onBackPressed()메소드가 바로 그것이다.  

### Activity 생명주기  
백스택. 작업들은 스택처럼 쌓이고 추가되는 애들은 스택 맨 위에 배치됨  
뒤로가기나 finish()실행하면 맨 위의 작업이 pop되고 그 아래있던게 스택의 맨 위가 된다.  

활동 상태는 크게
Running, Paused, Stopped, Destroyed  
이렇게 네 가지 있다.  
백스택의 맨 위에 있고 실행중인 상태가 <b>Running</b>이다.  
Activity가 맨 위에 존재하지는 않지만 아직 화면에 표시되고 있으면 <b>Paused</b> 상태이다. 화면 일부만 차지하는 TextBox같은게 그 예시이다. 계속 표시되기에 언제든 Activity를 재사용 가능하다. 다만 메모리 너무 부족하면 상태를 정리하려함  
만약 Stack이 맨 위에 있지도 않고 사용자에게 보이지도 않는 상태면 <b>Stopped</b> 상태이다. Activity의 상태와 변수는 유지하지만 메모리 부족으로 인해 정리될 수 있다.  
Activity가 완전히 Stack에서 Pop되어 파괴된 상태를 <b>Destroyed</b>라고 한다. 시스템에선 다른 앱을 쓰기 위한 메모리 확보로 
Destroyed 상태의 activity를 정리하도록 하는것이 바람직하다. 

Activity의 생명주기마다 실행할 수 있는 콜백메소드가 존재한다.  
onCreate(), onStart(), onResume(), onPaused(), onStop(), onDestroy(), onRestart() 이렇게 존재한다.  
각 메소드들마다 Log를 배치하여 어느 시점에 저 생명주기들이 불려지는지 확인할 수 있다.  
onCreate()는 초기화될때, onStart()는 활동이 화면에 보일때, onResume()은 스택 맨위에 있고 상호작용가능한 준비가되어 실행중일때, onPaused()는 다른 Activity가 시작되거나 재개되어 화면상에만 띄워져있을 경우, onStop()은 다른 활동에 의해 활동이 보이지않는 경우(대화상자같은경우로 인해서는 onPaused()가 호출됨), 활동소멸바로 직전에 onDestroy(), 활동 중지에서 실행으로 상태 바뀔때 onRestart()  

생성과 소멸은 onCreate(), onDestroy()  
사용자 화면에 보이는건 onStart()와 onStop()  
사용자와 상호작용 가능한건 onResume()과 onPaused()  

### 대화 TextBox처럼 띄우는 Activity  
AndroidManifest에서 Activity의 theme를 Theme.AppCompat.Dialog 식으로 바꾸면,  
Dialog식 Activity로 전환된다.  

### Activity 재활용 (정리)  
Acitivity가 Stop상태가 되면 Recycle할 수 있다.  
Activity_1에서 Activity_2를 실행하고 1이 Stop상태가 되었는데 만약 메모리가 부족하면 1은 Recycle되어버릴 것이다.  
메모리가 부족하지 않았다면 onRestart() 되겠지만, 만약 정리되었다면 Destroyed된 것이나 다름없기에 onCreate가 다시 호출될 것이다.  

이 자체는 문제 없어보이지만, Activity_1에 만약 입력해둔 데이터가 있다면 사라질 것이다.  
이를 저장하기 위해 onSaveInstanceState()가 존재한다.  
onCreate()메소드에 Bundle?타입으로 기본적으로 들어가는걸 볼 수 있다.  

onSave...메소드에 put타입("변수명", 데이터값)으로 데이터 저장하고  
onCreate()메소드 내에 있는 saveInstance....를 활용한다.  
기본적으로 null값이 들어가고 있었겠지만 만약 우리가 onSave...()메소드를 오버라이딩하여 put타입으로 값을 넣었다면 그 값을 get타입("변수명")으로 가져올 수 있게된다.  

이 방법은 Intent에서 데이터 가져오는 것과 매우 유사  
화면 회전할때도 데이터가 손실되는데 이건 다른방법으로 해결하겠음...(추후 알려줌)  

### Activity의 실행모드 (Launch Mode)  
AndroidManifest에서 activity의 launchmode를 변경할 수 있다.  
크게 standard, singleTop, singleTask, singleInstance 이렇게 네 모드가 있다.  
- Standard(표준) : 우리가 지금까지 구현할 활동들.  
백스택을 활용하여 활동을 관리하고 새 활동 시작하면 스택의 맨 위로 올라간다. Activity가 시작할때 새 instance가 생성된다.  
Standard의 경우엔 Activity를 시작할 때마다 새로운 instance가 생성되어 FirstActivity타입으로 여러 instance가 생성될 수 있다. 그러면 스택엔 FirstActivity가 여러개 쌓이는것이다.  
- singleTop : 스택 맨 위에 이미 Activity instance가 존재하면 새 인스턴스를 만들지 않고 기존 instance를 사용하는 방법이다.  
먼저 AndroidManifest의 activity:launchMode를 singleTop으로 변경  
여러번 Activity를 시작해도 하나의 instance만 스택 맨 위에 존재한다.  
다만... 만약 다른 Activity가 스택의 맨 위에 존재할때는 Standard처럼 새로운 instance를 생성한다.  
- singleTask : 하나의 Activity instance만 허용하고 싶다면 이 방법을 사용한다.  
이 방법은 실행될때마다 시스템에 백스택에 Activity instance가 존재하면 전부! 모두 pop하고 이 instance를 재사용하는 방법이다.  
- singleInstance : 가장 복잡한 모드이다.  
시스템은 이 활동 관리를 위해 새로운 백스택을 만든다. 이 새로운 백스택은 공유됨  
실제로 taskId를 비교하면 singleInstance를 사용한 Activity만 다른 taskId를 가짐  

### 현재 Activity 확인?  
기존에 우리가 Activity들에 상속하는 AppCompatActivity()도 새롭게 다른 클래스로 만들 수 있다.  
예를들어 BaseActivity()라는 클래스를 만들고 AppCompatActivity()를 상속받은뒤,  
입맛에 맞게 메소드들을 재정의하고 AppCom...대신 BaseActivity()를 상속받으면,  
기존 AppCom...에서 사용하는 기능과 더불어 새롭에 우리가 추가한 메소드들도 사용할 수 있다.  

물론 Activity들에 상속받아 가져오는 BaseActivity()에서 재정의한 내용보다  
따로 Activity들에서 재정의하는게 우선적으로 사용된다. (자식의 재정의가 우선)  
참고로 BaseActivity는 open형으로 만들어야 상속이 가능하다는 점 잊지 않길.  

### 어디서나 앱 종료  
앱 종료를 어디에서나 하고싶다? 뒤로가기 여러번해서 앱 종료하기 싫다?  
모든 활동을 참조하는 컨트롤러를 만들어서 앱들의 Activity들을 통괄하여 관리할 수 있다.  
singleton을 사용하여 가능한데,  
우리는 object라는 기능으로 이것을 가능캐한다.  

singleton이기에 어디에서나 전역적으로 사용가능하고, object에서 정의한 메소드에서 Activity를 받아 List로 정렬하고 이곳에 Activity들을 추가하고 제거하도록 코드를 작성하면 Activity들을 한번에 관리가능하다.  

이렇게 모든 Activity를 받을 수 있는 object(싱글톤)을 만들고 BaseActivity() onCreate()에 포함시키면 모든 Activity들이 object를 사용 가능할 것이다.  

### Activity를 시작하는 다른 방법들...  
intent를 만들거나 startActivity()나 startActivityForResult()와 같은 방법을 통해 여러 방법으로 Activity를 시작하곤 했다.  
intent값을 전달받아 startActivity()에 넣을수도 있고...  

object는 클래스 전체가 하나의 싱글톤객체,  
companion object는 클래스 내에 일부분이 싱글톤 객체로 선언.  
인자값을 받아서 intent 전달을 도우면서 Activity 시작까지 안에 만들어놓으면..  
우린 companion object에 있는 이 메소드를 실행시키는 것만으로도 새로운 Activity를 intent값과 함께 시작할 수 있다.  

### with, run, apply  
with(객체()) {객체명.메소드를 생략가능..  
메소드()  
메소드()  
}  
이렇게 가능하다.. 반복사용을 막음  

run은 with와 유사. 구문만 다름  
대신 직접호출이 안되어 obj.run처럼 실행함수를 호출해야한다.  
val result = StringBuilder().run {...}  

apply는 객체에 적용되는건 run과 유사한데,  
<b>객체 자체만</b> 반환한다. 따라서 대입되는 값은 obj이다.  
val result = StringBuilder().apply {...}  
하면 result에 들어간 값은 무조건 람다식 내의 메소드들이 apply가 된 StringBuilder() 객체이다.  
따라서 with나 run은 람다식 내에 toString()이 있으면 result에 toString()값이 들어갔겠지만,  
apply는 result에 반환된 object를 활용하여 result.toString()처럼 직접 사용해야한다.  

### 정적 메소드 정의 static method  
자바에서 public static void a(){}  
이런 방식으로 정적 메소드 선언을 했었다.  
Kotlin에서는 object를 사용하여 전역에서 사용가능한 정적클래스 혹은 메소드를 선언할 수 있다.  
일반 클래스에서 메소드만 정적으로 쓰고싶다면 메소드 내부에 companion object를 사용하면 된다.  
정적메소드로 선언되지않은건 클래스가 생성되고나서야 메소드 사용이 가능한데, 클래스 내부에 companion object가 선언되어있으면 클래스명.메소드명()으로 바로 사용가능하다.(syntax sugar때매)  

싱글톤이나 companion object 메소드에 @JvmStatic 애노테이션 추가하면 Kotlin컴파일러가 이걸 실제 정적메소드로 컴파일한다. *단 싱글톤이나 companion object메소드만 애노테이션 적용가능*  
이렇게 실제 정적메소드가 되면 java랑 kotlin모두 클래스명.메소드명()으로 companion object를 부를수있다.  

패키지에 함수를 넣고 패키지를 호출하여(import) 사용하게 하는방법도 있다.
패키지명.메소드명() 가능?  


## 4장  
### UI  
레이아웃을 활용하여 UI를 만들 수 있다.  
ConstraintLayout이라는거 최근에 생기긴했는데 수동코딩에 적합하진 않음. 대신 visual editor에서 드래그앤드롭으로 쉽고 개발가능    

layout_width와 layout_height 속성으로 레이아웃 크기를 지정할 수 있다.  
이 값들은 match_parent, wrap_content, 고정값 이렇게 3가지 가능  
고정값으로 할 때는 dp로 입력한다.  
dp가 display에 크기에 맞게 조정돼서 다양한 휴대폰 해상도에 잘 적응됨  

Layout에는 위젯들을 추가하여 다양한 기능을 화면에 표시가능  
텍스트 표시는 TextView태그, 버튼은 Button태그 등...  
gravity 속성을 통해 위젯 내의 값들의 위치를 조정할 수 있다.  
center하면 중앙정렬, top은 위, bottom은 아래, start는 기초인가..?, end는 젤 오른쪽아래..? 기호 ('|')를 써서 여러 정렬을 함께 사용할 수도 있다. 예를들어 화면 정중앙에 넣고싶으면 center_vertical|center_horizontal 처럼? (근데 center가 이거 두개 다 정렬한 역할임)
layout_gravity를 쓰면 Layout에서의 위치 조정가능  

Text를 사용하는 <b>TextView</b>의 경우엔 textColor이나 textSize같은 속성도 있다.  
Button 태그에는 text속성으로 버튼내에 적힐 글자를 넣을 수 있다.  

<b>Button</b>의 경우에 Activity에 View.OnClickListener 구현받고 onClick()메소드 구현하면 메소드 내의 코드가 setOnClickListener이 실행될때 반응함  

<b>EditText</b>라는 위젯은 사용자가 입력할 수 있는 텍스트입력창을 만들 수 있다.  
hint 속성으로 아무것도 입력되지 않았을 때 보이는 글자를 표시할 수 있다.  
만약 height를 wrap_content로 해둘때 생기는 문제는, 글자가 여러개 써서 여러줄이 되면 점점 크기가 늘어난다는 단점이 있다.  
그래서 maxLines를 설정하여 과하게 칸이 늘어나는것 방지 가능하다.  

버튼 위젯과 함께 사용하여 버튼을 눌렀을 때 editText에 적힌 글자를 toString()하여 변수에 넣고, 그 변수를 Toast.makeText().show()하여 토스트메세지로 출력할 수 있다.  
editText.text에 getText와 setText가 들어가있음.  

<b>ImageView</b>는 UI에 이미지를 표시할 때 사용한다.  
res폴더 내에 drawable폴더가 있는데, 이 안에 이미지들을 넣어 사용한다.  
대부분 휴대폰은 해상도가 xxhdpi거나 더 높기때문에 drawable-xxhdpi 처럼 폴더를 직접 생성해주어야한다.  
이렇게 drawable폴더를 만들고 img파일을 집어넣었다면, ImageView태그 속성에 src를 통해 @drawable/사진명 을 기입한다.  
Activity파일에서 imageView객체에 .setImageResource(R.drawable.사진명2)를 하여  
다른 이미지로 설정할 수도 있다.  

<b>ProgressBar</b>는 진행상태를 나타내는 위젯이다.  
기본값으로 동글동글 돌아가는 형태인데,  
style속성을 변경하여 다른 형태로 바꿀수도 있다. style="?android:attr/progressBarStyleHorizontal"  
만약 막대 progressBar에 max속성을 추가하면 0부터 max값까지의 단계를 갖는 위젯이 된다.  
progress위젯은 visibility 속성을 사용하여 숨기거나 나타내거나 할 수 있는데, 기본값은 visible(보임)이다.  
Activity 코틀린 코드로도 visibility의 상태를 바꿀수있는데, View.VISIBLE 혹은 View.INVISIBLE 그리고 View.GONE으로 변경할 수 있다.  
setVisibility() 메소드로 변경할 수도 있고, 직접 객체명.visibility를 값변경 할 수도 있다.  

<b>AlertDialog</b>는 Dialog팝업창 위젯이다.  
Activity위에 일정크기로 나타난다.  
매우 중요메세지나 위험메세지를 나타낼때 쓴다.  
정말 중요한 파일을 지울때 확인하는 용도로 쓰이곤 한다.  
apply구문을 사용하여 AlertDialog객체의 Builder()객체를 사용할수도 있다.  
AlertDialog.Builder(this).apply{...}  
저 식 내부엔 setTitle(), setMessage(), setCancelable[뒤로가기로 취소가능한지 true or false], setPositiveButton("메세지"){dialog, which  -> 목적지함수}  
setNegativeButton("메세지"){dialog, which -> 목적지함수}  
show()
이런 식들을 통해 바로 설정가능. 두개의 버튼으로 어떤행동이 취해질지는 따로 설정해야함  

### 기본 레이아웃들  
레이아웃은 위젯배치를 위해 있는 컨테이너(Container)이다. 레이아웃 내에 레이아웃을 임베디드 할 수 있다. 위젯은 레이아웃 내에 있을 수 있다.  
즉, 레이아웃 끼리도 포함 가능하고, 레이아웃은 위젯을 포함할수 있다.  
대표적인 Layout들을 여기서 소개한다.
- LinearLayout : 일반적으로 사용하는 레이아웃. 내부에 위젯을 세로or가로로 배치.  
orientation속성을 통해 horizontal(가로) 혹은 vertical(세로)로 방향설정 할 수 있다.  
내부에 추가되는 레이아웃들은 여기서 설정한 방향에 맞게 정렬된다.  
방향이 horizontal이면 width가 match_parent가 될 수 없다. 다른 위젯이 들어갈 수 없기에..  
마찬가지로 vertical이면 height가 match_parent 불가능이다.  
layout_gravity 속성은 레이아웃 속의 위젯들을 어떻게 정렬할지를 위해 사용한다.  
따라서 orientation에 따라서 만약 가로정렬이면 다른 위젯들을 의식하여 가로쪽으론 정렬이 안된다. center정렬하면 가로위치는 같고 세로위치가 중앙정렬됨.  
위젯 크기를 백분율로 설정하기 위해서 사용하는 weight 속성도 중요하다.  
대신 이걸 쓰기 위해선 width를 0dp로 설정해야한다(vertical은 height를 0으로)  
weight는 비율을 나타내는것이다.  
- RelativeLayout : 상대적위치정렬을 사용하는 레이아웃이다.  
layout_alignParentLeft="true"이런것처럼 위젯들 내부에서는 parent(레이아웃)을 기준으로 위치를 설정한다.  
참조가능한 값들은 layout_alignParentLeft, layout_alignParentTop, layout_alignParentCenter 등..가능하다.  
이처럼 Parent를 기준으로 위치설정도 가능하지만,  
layout_above, layout_below, layout_toLeftOf 등과 같은 속성을 사용하여 다른 위젯 위치를 참조할 수도 있다. 참조방법은 "@id/위젯id" 이런식으로..  
*주의* 위 예시처럼 위젯이 위젯을 참조하는 경우에는 참조받을 위젯을 먼저 선언해야한다. 그래야 id를 찾을수있으니까.  
- FrameLayout : '모든' 위젯을 기본값으로 레이아웃 상단왼쪽 모서리에 배치하는 레이아웃이다.  
구석에 다 몰아넣어놓고 정의되는 순서대로 차곡차곡 위로 쌓인다.  
gravity값을 주어 정렬하는 레이아웃이다.  


참고로 위젯들은 다 상속관계가 존재한다.  
예를들어, View를 상속하는 TextView, ImageView, ViewGroup 세가지로 나뉘고,  
TextView를 상속받는 EditText와 Button이 있다.  
그리고 ViewGroup을 상속받는 LinearLayout과 RelativeLayout.. 이런식으로...  
그래서 위젯마다 사용가능한 메소드들이나 속성이 조금씩 다른것이다.  
이걸 이해한다면, 우리는 Customize된 위젯을 만들 수도 있다.  
원하는 기능을 가진 상위계층 위젯을 상속받아서 새로운 위젯을 만들고, 그 위젯을 활용할 수 있다.  

### 레이아웃 포함 include  
레이아웃을 미리 만들어두고, 다른 레이아웃에서 이전에 만들어둔 레이아웃을 include시킬수도있다.  
이 방식을 사용하면 어딜가든 기본적인 Layout을 포함시키면서 Layout을 설계할 수 있다.  
include layout="@layout/title"태그로 title.xml이라는 이름으로 저장되어있는 layout 내용을 그대로 가져온다. import라 생각하면 편함  

만약 Activity에 상위 nav바에 대한 내용이 있으면 supportActionBar?.hide()로 숨길 수 있다. [없을수도있으니 ?붙임]  

### custom 위젯 만들기  
class NewLayout(context:Context, attrs:AttributeSet):상속받을layout(context, attrs)  
이렇게 class를 선언하고 그 안에 init을 통해  
LayoutInflater.from(context).inflate(R.layout.title, this) 를 넣는다.  
그러면 원하는 위젯들이 들어있는 새로운 레이아웃 기능을 그대로 끌어쓸 수 있다.  
이렇게 만든 위젯들이 담긴 레이아웃을  
우리가 쓸 Activity의 layout에서 com.example.프로젝트명.NewLayout 같은 태그를 통해 위젯처럼 추가하면 된다.  
마치 레이아웃 내에 위젯을담은 레이아웃을 넣은 느낌?  

전체이름이랑 패키지명을 넣어야하는점 빼면 시스템 위젯을 추가하는것과 똑같다!  
Activity 안에서 위젯처럼 넣은 레이아웃 내의 위젯들을 맘대로 가져다 쓸 수 있다.  

### ListView 위젯  
ListView는 위젯을 추가하고 Activity내에서  
listView.adapter = 리스트...  
를 통해 리스트를 listView 위젯에 연결해주고  
이를 화면에 보여주는 위젯이다.  
여기서 list를 가져오는 방법이 중요?  
ArrayAdapter<타입>()을 사용하여 리스트를 입력받아 특정 item이 담긴 list에 대한 layout에 입력받는것도 가능하다.  

> Text로만 리스트 받는것도 가능하지만 ListView도 UI customize가 가능하다.  

fruit_item이라는 xml 레이아웃을 만들고  
그 안에서 ImageView와 TextView위젯을 추가한다.  
그리고 ArrayAdapter을 상속받는 새로운 Adapter클래스를 만들고, getView를 오버라이딩하여 이미지와 텍스트 두가지를 모두 입력받아 view로 반환하는 메소드를 만든다.  

이제 새롭게 정의한 fruitList에 Text와 사진파일을 모두 담고 새롭게 정의한 Adapter를 사용하여 목록으로 띄운다.  

repeat(숫자)이라는 메소드는 숫자만큼 반복하는 메소드이다. 그냥 참고로..  

### ListView 효율성의 최적화?  
현재 방식은 스크롤할때마다 계속 불러오는 형태인데, if (convertView==null)일때만 생성하고, 그게아니면 view=convertView로 새로고침만 해주게하면 메모리 낭비를 막을 수 있다.  
하지만 아직 getView()가 호출될때마다 findViewById()가 계속 호출된다.  
이건 ViewHolder라는것을 사용하여 한번 호출된 이미지와 Text를 ViewHolder로 값을 잡아두고, view.tag에 저장한다.  
그리고 갱신될때는 view.tag as ViewHolder를 사용해 viewHolder에 다시 넣어둔다.  

### ListView활용  
단순히 리스트만 보여주는게 아니라, listView를 클릭할때 이벤트가 생기도록 할 수도 있다.  
setOnClick....을 사용하면 되는데,  
parent, view, position, id값을 모두 받고 그거에 맞는 메소드를 실행시키는데,  
우리는 position만 다르지 parent, view, id값은 모두 같기때문에 언더바를 사용하여 표현 가능하다.  
_,_,position,_ -> 이렇게...  

### RecyclerView  
나름 최근 위젯중에 이런 위젯도 있다.  
build.gradle에서 recyclerview에 관한거 구현해놓으면 모든 버전에서 사용가능  
activity_main 레이아웃에 위젯으로 RecyclerView를 먼저 추가. 패키지 경로 완전한 이름으로 넣어야함.(시스템SDK에 없어서)  
이것만으로 ListView의 이미지, fruit클래스, fruit_item.xml 재사용해서 중복작업줄임  

FruitAdapter와 ViewHolder Recycler.Adapter<어댑터.ViewHolder>() 상속받고  
안에 ViewHolder도 RecyclerView.ViewHolder(view)로 상속받고...  
LinerLayoutManager(this)로 선언하고  
recyclerView:RecyclerView=findVi..선언하고  
recyclerView.layoutManager=layoutManager  
val adapter = FruitAdapter(fruitList)  
recyclerView.adapter = adapter  
이런식으로...  

RecyclerView는 가로 스크롤도 지원한다.  
과일아이템 xml을 vertical로 변환하고  
너비를 80dp로 사용..  
imageView와 textView layout_gravity를 center_horizontal로 하고 layout_marginTop으로 여백 확보  
나중에 Activity에서 layoutManager.orientation=LinearLayoutManager.HORIZONTAL  
설정...  

이 외에도 GridLayoutManager나 StaggeredGridLayoutManager도 있음.  

대신 RecyclerView는 이벤트를 제공하지 않는다. 구현도 어렵다.  


### 이미지 구축..?  

