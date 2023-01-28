# 스프링 핵심원리 기본편 - 김영한 강사  

6주차 학습 목표 : 섹션 1, 2(중반)  
도입에 앞서 스프링의 핵심가치는 객체지향 프로그래밍에 있다.  
본 강의는 스프링이 왜 생겨났고, 어째서 이러한 기능을 제공하는지에 대한 이유와 핵심원리를 다룰 것이다.  

ㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡ  

## 섹션 1 - 객체 지향 설계와 프로그래밍  

### 스프링의 탄생배경  
과거엔 J2EE(EJB)라는 이론은 좋지만 어렵고 복잡하며 느린 기술이 존재했다.  
대체하기엔 이론이 너무 좋아서 이걸 사용 많이 했었고, 죽어나가는 것은 개발자였다.  
그러던 중 '로드 존슨'이라는 한 개발자가 EJB에 대한 비판을 책으로 담으며 이것에 대한 대체 가능한 고품질 예제 코드들을 책에서 선보였는데, 이것이 추후 우리가 아는 Spring이 된다.  
'개빈 킹'이라는 개발자도 있었는데 EJB의 서버에 답답함을 느껴 Hibernate라는 오픈소스를 만들어 배포하였고 이것이 인기가 너무 많아져서 EJB를 만든 자바 측에서 이 개발자를 고용하여 JPA라는 것을 만들고 표준으로 하여 현재까지 이어져 오고 있다.  
다시 스프링의 역사로 넘어와서.. 2002년 로드 존슨의 책이 출간되고 유겐 휠러, 얀 카로프 라는 두 개발자가 로드 존슨에게 오픈소스 프로젝트를 제안하였다.  
전통적인 EJB라는 혹독한 겨울을 넘어 새로운 시작(봄)을 의미하는 의미에서 Spring이라는 이름이 탄생하였다.  
그렇게 2003년 스프링프레임워크 1.0이 출시되었고, 이후 계속하여 업데이트를 내다가 2014년에 설정이 어려운 스프링을 위해 스프링부트가 등장하여 설정이 매우 편리해졌다.  

### 스프링이란 그럼 무엇일까? --> 여러 기술들의 모음집!  
스프링프레임워크와 스프링부트는 필수지만, 그 외에 프로젝트들을 이것저것 선택하여 사용하여 스프링 시스템을 만든다. 예를 들어 스프링데이터, 스프링세션 스프링시큐리티, 스프링RestDocs, 스프링배치, 스프링클라우드 등...  
스프링프레임워크가 가장 중요하다.  
그 안에는 스프링의 핵심 기술인 스프링DI컨테이너, AOP, 이벤트 등이 있다.  
웹 기술(스프링MVC, 스프링WebFlux)도 있고 그 외에도 데이터접근 기술(트랜잭션, JDBC, ORM지원, XML지원)이나 기술통합(캐시, 이메일, 원격접근, 스케줄링), 테스트, 언어(코틀린, 그루비)가 있다.  
최근엔 스프링부트로 인해 스프링프레임워크 기술을 편리하게 사용할 수 있게 해준다. (최근엔 스프링부트를 기본으로 사용할 정도)  
스프링이 어떠한 언어이고, 왜 만들어졌는지 아는 것은 중요!  
스프링은 자바 언어기반 프레임워크인데, 자바의 큰 특징은 바로 '객체 지향 언어'.  
이러한 객체지향언어의 특징을 강력히 살려내는 것이 스프링이라는 프레임워크의 목적이다. 즉, 좋은 객체지향 어플리케이션을 만들기 위한 프레임워크라는 것이다.  

### 그럼 좋은 객체지향 프로그래밍은 무엇인가?  
먼저, 객체지향프로그래밍은 프로그램을 유연, 변경용이하게 만들어준다.  
이것이 바로 '다형성'이다. 역할과 구현으로 구분하는 것이다.  
운전자라는 역할이 있고 자동차라는 역할이 있다. 자동차가 바뀌어도 운전자에게는 영향이 없음! 새롭게 무언가를 배워야하지 않는다. 운전자는 운전면허증만 있으면 다른 자동차를 타는 데에 문제가 생기지 않는다.  
이를 프로그램으로 따지면 클라이언트(운전자)에게 영향을 주지 않고 새로운 기능의 프로그램(자동차)을 제공할 수 있도록 하는 것이다.  
공연으로 따지면 뮤지컬이 하나 있고, 그를 연기하는 배우가 있다고 가정하자.  
여기서 배우가 아무리 바뀌어도 이 작품의 스토리는 바뀌지 않는다.  
이처럼 역할과 구현으로 구분하면 문제를 단순, 유연하고 변경용이하게 된다.  
클라이언트는 대상의 역할(인터페이스)만 알면 된다. 자동차로 따지면 엑셀을 밟아서 앞으로 나아가는 이동수단이라고 알면 됨.  
자바언어에서 이런 다형성을 사용하면, '역할=인터페이스' '구현=인터페이스를 구현한 클래스, 구현 객체'이다. 구현보다 역할이 더 먼저되고 중요함.  
혼자 있는 객체란 없다. 클라이언트가 요청하면 서버가 응답하는데, 객체들끼리 서로 요청하고 응답할 수 있다.  
자바의 다형성에 '오버라이딩'도 꼽을 수 있다. 메소드를 재정의하는 것으로, 오버라이딩된 메소드가 실행되어 클래스마다 같은 동작을 명령해도 다른 결과를 낼 수 있다. 즉, 실행시점에서 유연하게 변경이 가능해지는 것이다.  
클라이언트가 여러 서버 중 하나를 골라서 연결시키면, 똑같은 명령이라 해도 다른 서버에서는 또다른 결과를 낼 수 있다.  
즉, 다형성 덕분에 역할과 구현으로 나누고, 유연해지고 변경용이해지고 확장이 가능해지고 클라이언트에 영향을 주지 않을 수 있다. 그만큼! 인터페이스를 잘 짜는게 제일 중요하게 될 것이다.  
단점도 있으니.. 역할(인터페이스) 자체가 바뀌면 클라이언트랑 서버 둘다 엄청난 변경을 필요로 할 것이다. 마치 비유하면 이동수단을 자동차에서 갑자기 비행기로 바꾸는 것이나 다름없음.  
스프링에서도 객체지향에 '다형성'이 가장 중요하게 사용된다.  
스프링은 이러한 다형성을 극대화하여 이용하도록 도와준다. IoC(제어역전)라는 것과 DI(의존관계주입)는 다형성을 사용한 역할와 구현을 편리하게 해주는 것.  

### 좋은객체지향설계에 5가지 원칙이 있는데 이것을 SOLID라고 한다.  
로버트마틴이라는 개발자가 좋은객체지향프로그래밍 5원칙을 정리함.  
- SRP(Single Responsibility principle) : 단일 책임 원칙 - 하나의 클래스는 하나의 책임만 가진다. 기준은 '변경'. 변경이 있을 때 파급 효과가 적게 짠 코드가 SRP를 잘 지킨 것.  
- ☆OCP(Open/Closed principle) : 개방-폐쇄 원칙 - 확장에는 열려있으나 변경에는 닫혀있어야 함. 확장하려면 기존 코드를 변경해야하지 않나? 라고 생각할 수 있으나, 인터페이스를 사용한 다형성을 보면 그것이 가능하다는 것을 알 수 있다.  
근데 다형성을 사용하더라해도 클라이언트 코드를 변경하긴 해야하지 않는가? OCP가 깨짐  
이 문제를 해결하기 위하여 객체를 생성, 연관관계 맺는 별도의 설정자가 필요하다.  
- LSP(Liskov substitution principle) : 리스코프 치환 원칙 - 다형성을 적용한 하위 클래스는 인터페이스의 규약을 다 지켜야한다. 예를들어 엑셀레이터라는 인터페이스는 앞으로 가는 것을 목표로 하는데, 뒤로가게 구현하면 LSP의 위반이다.  
인터페이스가 목표로 하는 규약이 있으면, 그것을 맞춰서 기능적으로 보장해야하는 것.  
- ISP(Interface Segregation Principle) : 인터페이스 분리 원칙 - 범용 인터페이스 하나보다, 특정 기능의 인터페이스로 분리하여 여러개로 두는게 더 낫다.  
- ☆DIP(Dependency Inversion Principle) : 의존관계 역전 원칙 - 추상화에 의존해야지 구체화에 의존하면 안된다. 구현 클래스에 의존하지 말고 인터페이스에 의존해야 한다.  
즉, 역할과 구현에서 역할설정이 더 중요하기에 역할을 설정하는 데에 노력을 기울여야하지 구현하는 데에 큰 비중을 두면 안 된다.  
위에서 설명한 뮤지컬로 따지면 배우가 바뀐다고 작품을 할 수 없으면 안 된다. 어느 배우가 하더라도 뮤지컬 스토리가 똑같이 적용되도록 해야 하는 것이다.  
구현체에 의존하면 변경이 매우매우 어려워진다. 사실 우리가 했던 MemberRepository m = new MemoryMemberRepository(); 도 MemberService를 인터페이스로 의존하면서 구현체인 MemoryMemberRepository에도 의존하는 DIP 위반 상황이다.  
그런데 이걸 지키려고 구현체 의존을 안하면 구현체가 없는데 어떻게 코드가 돌아가는가? 즉, 다형성만으로는 OCP, DIP를 지킬 수 없다. 무언가 더 필요하다.  

### 스프링은 다형성+OCP,DIP를 가능하게 지원해주는 기술이다.  
DI(Dependency Injection) : 의존관계, 의존성 주입  
스프링이 없던 시절에 OCP, DIP를 지키면서 개발해보니 너무 할 일이 많았고, 그래서 프레임워크로 만들어버린 것이다.  
섹션 2에서는 코드를 직접 짜보며 스프링이 왜 만들어졌는지 확인할 것이다.  
정리하면, 이상적으로는 모든 설계에 인터페이스를 부여해야한다.  
하지만 추상화라는 비용이 발생하기에, 기능 확장이 필요하면 인터페이스를 쓰고 아예 기능확장을 쓸 가능성이 없으면 구체 클래스를 직접 작성하는 것이 좋은 방향이다. 향후 필요하면 인터페이스 사용.  

ㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡ  

## 섹션2 - 프로젝트 생성  
순수 자바코드로 짤 예정이기에 스프링부트 스타터로 파일만 만들어주었다.  
나의 경우엔 스프링부트3.0.2, 자바17로 프로젝트 생성을 진행하였다.  

### 구현할 것의 요구사항  
회원(가입기능, 조회기능, 등급제, 자체DB구현 가능하고 외부 시스템 연동도 가능), 주문과 할인 정책(회원은 상품구매 가능, 등급에 따른 할인정책, 할인 정책은 바뀔 수 있음 - 최악의 경우 적용 안할수도..)  
이러한 요구사항이 넘어왔을 때, 할인정책 같은것을 지금 당장 구현하기에 어려움이 따라보인다. 그렇다고 결정이 될 때까지 기다리기만 하는 것도 어려운 상황이다.  
이럴 때 인터페이스를 사용하여 구현체를 언제든 갈아끼울 수 있도록 한다.  
(현재는 스프링 없이 자바만으로 개발을 해 볼 예정이다.)  

### 회원 도메인 설계     
회원 저장소라는 인터페이스. 이것에 대한 구현체(메모리 회원 저장소, DB 회원 저장소, 외부 시스템 연동 회원 저장소)를 세가지 중에 하나를 선택하여 실행할 수 있도록 할 것임. 일단 개발은 메모리로 하고 나중에 DB나 외부시스템으로 갈아끼울 예정.  
회원서비스를 인터페이스로 만들고, 이를 구현하고 그 구현체와 회원저장소 인터페이스를 연결한다.  
일단 실제 참조는 '클라이언트 -> 회원서비스 -> 메모리회원저장소' 모양이 될 것임.  
### 회원 도메인 개발  
### 회원 도메인 실행과 테스트  
### 주문과 할인 도메인 설계  
### 주문과 할인 도메인 개발  
### 주문과 할인 도메인 실행과 테스트  