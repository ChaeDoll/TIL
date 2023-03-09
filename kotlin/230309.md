# Kotlin (코틀린) 언어 공부
### 변수 선언  
일반 변수 선언 : var  
final 변수 선언 : val  
> 코틀린에서는 nullable 명령어를 ? 하나로 생략할 수 있다.  
변수 타입 뒤에 ?를 붙일 시에 값이 'null이 될 수도 있다'라고 선언하는 것이다.  
?를 붙이지 않으면 null값이 들어올 때 오류가 나지만, ?를 붙이면 null값을 인식하고 반환할 수 있다.  

### 형 변환  
to변수()를 통해 형 변환을 할 수 있다.  
var a : Int = 32  
var b : String = a.toString()  
이렇게 하면 a의 32값이 String 타입으로 변환되어 변수 b에 저장된다.  

### 배열  
특정 값을 넣어서 배열을 선언하고 싶을땐 arrayOf를 사용한다.  
타입을 지정하지 않고 생성하면 어떠한 타입이 들어가도 상관없다.  
> var a : Array<타입> = arrayOf(값1, 값2, 값3) 이고,  
타입을 지정안해서 var b = arrayOf(1, "awe", 1.66) 하는 것 가능함 (자동으로 Array<Any>타입이 되는 것)  
var c = arrayOf<타입>(값1, 값2, 값3) -> 이 방법은 제네릭 방법을 사용한 것.  
혹은 기본 함수를 사용하여 var d = intArrayOf(100, 200, 300) 방식도 가능  

크기를 정해서 
> var a = Array(크기, {들어갈 값}) or Array(크기){들어갈 값} 으로 표현할 수도 있다.  
예시 : var b = Array(10, {0}) -> 배열 b에 0이 10칸 들어감  
var c = Array(10, {i->i*5}) -> 배열 c에 인덱스x5의 값이 10칸의 자리에 채워짐  
var d = Array(5, {""}) -> 배열 d에 공백이 5칸 채워짐  

arrayOfNulls<타입>(값, ...) 을 사용하면 없는 값이 나올 때 오류 대신 null값이 반환됨  

### 함수  
> fun main() {  
    print(add(1,2,3))  
}  

- fun 함수명(변수명: 타입): 반환타입  


> fun add(a: Int, b: Int, c: Int): Int{  
    return a+b+c;  
}  

기본적인 함수는 이런 모양이다.  
반환형이 모두 같기에 fun add(a:Int, b:Int, c:Int)=a+b+c 도 가능하다  

### 조건문  
if는 다른 언어랑 사용하는 방법이 동일하다.  
is라는 것이 있는데 데이터 타입 비교에 사용된다.  
예를 들어 if(a is Int) 이면 참이다.  
when이라는 명령어는 switch문과 유사하다.  
> when(a){  
    1 -> print(a)  
    "awd" -> print(a)  
    else -> print(a)  
}  

a값을 받아서 아래 조건에 만족하면 그 우측에 있는 코드를 실행시킨다.  

### 반복문  
while은 다른 언어랑 사용이 동일하다.  
for은 for(i in 0..3) 이면 i가 0부터 3까지 반복한다.  
for(i in 3 downTo 0) 이면 i가 3부터 0까지 하향 반복한다.  
for(i in 0..5 step 2) 이면 i가 0부터 2까지 2개 간격으로 반복한다.  
for(i in 'a'..'e')이면 i가 a부터 e까지 반복한다.  

### 흐름제어  
break, continue는 다른 언어와 사용이 동일하다. break; 혹은 continue;  
추가 기능으로, 반복문 앞에 '라벨명@'을 붙이고 break나 continue문에  
'@라벨명'을 붙이면 break 혹은 continue가 라벨 위치에서 실행된다.  
예시 : allSkip@for(i in 0..10) {.... ... break@allSkip}  

### 클래스  
코틀린은 자바와 다르게 생성자를 만들어주지 않아도 된다.  
객체 생성 시에 속성값을 넣어주기만 해도 된다.  
> class Test(var name:String, val birth:Int){  
    fun ha(){  
        println("$name $birth)  
    }  
}  
fun main(){  
    var a = Test("chaeyun", 24)  
    println("$a.birth $a.name)  
    a.ha()  
}  
이러면 a 변수가 Test클래스 객체가 되고 내부에 값으로 String 타입의 "chaeyun"과  Int 타입의 24가 저장된다.    
이후 print의 식으로 인해 a객체의 birth, name이 출력되고 a.ha()에서 a 객체의 메소드인 ha()가 실행되어  
name과 birth값이 출력된다.  

생성과 동시에 코드를 실행하도록 할 수 있는데,  
init이라는 코드를 통해 가능하다.  
class 내부에 init{}을 두어 구문이 실행되도록 할 수 있다. 참고로 init은 여러개 가능  

보조생성자로 constructor를 오버로딩 목적으로 사용할 수도 있다.  
대신 반환타입으로 this를 사용하여 기본생성자로 넘겨주어야 한다.  
예시 : 클래스는 Test(var name:String, val birth:Int)인데,  
constructor(name:String): this(name, 23)을 통해  
var a = Test("chaeyun") 만 입력해도 보조생성자를 통해 birth값이 23으로 대입된다.  

상속 기능을 사용하기 위해서는 부모 클래스가 open이라는 키워드를 사용해야한다.  
그리고 클래스 생성 시 : 부모클래스()를 붙여주면 된다.  
부모의 메소드를 사용하고 싶다면 super.메소드명()을 하면 되고,  
오버라이딩은 함수 앞에 override 단어를 붙이면 된다.  

추상클래스는 자바와 동일하게 abstract만 붙이면 된다.  

인터페이스는 자바와 다르게 추상함수 뿐만 아니라 일반함수도 선언 가능하다.  
하지만 생성자는 생성할 수 없다. 구현이 되면 open, 구현이 없으면 abstract로 동작  

### 접근제한자  
자바는 메소드에 아무것도 안붙이면 protected인데 코틀린은 public이 기본이다.  
public, protected, private 세 구문이 존재하는 것은 동일하다.  

### null 처리  
자바에서는 if(변수==null)이라는걸 쓸 때가 종종 있는데, 코틀린은 ?을 사용한다.  
a?.let{} -> a가 null이면 .let 뒤에 있는 구문을 실행 X  
b?:"default" -> b

...아 어렵다


