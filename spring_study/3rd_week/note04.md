섹션4 - 스프링빈과 의존관계  

회원컨트롤러가 회원서비스와 회원리포지토리를 사용하기 위해서는 이들 간의 연결이 필수적일 것이다. 이를 위하여 @Autowired라는 기능을 사용하는데, 이 명령어를 통해서 컨테이너의 서비스 혹은 리포지토리를 가져와 연결할 수 있다. 그리고 이것을 의존관계 주입(DI)이라고 한다.  

일반적으로 Controller에서 외부 요청을 받고, Service에서 비지니스 로직을 생성하고, Repository에서 데이터를 저장한다. 그렇기에 Controller -> Service -> Repository의 순서로 작업이 처리되는 것이 일반적이다. 이러한 의존관계를 주입하기 전에 먼저 스프링빈을 등록해야한다.  

스프링빈의 등록 방법은 두가지로, 아래에 적힌 방식들이 있다. 
1. 컴포넌트 스캔을 통해 자동 의존 관계 설정  
2. 자바 코드로 직접 등록  

컨테이너에 포함시키고 싶은것들에 @Component를 추가하여 빈으로 등록하는 방법이 있는데, 이는 @Component만 입력하면 되기에 등록할 때에 매우 간편하다는 장점이 있다. @Controller, @Service, @Repository라는 기능들도 사용할 수 있는데, 이 세가지의 기능 속에 Component가 포함되어 있기에 이것들도 컴포넌트 스캔 방식이라고 이야기 할 수 있다. 컴포넌트 스캔의 대상은 메인패키지 내부에 있는 경우에 스캔 대상이다.  

자바 코드로 직접 등록하는 경우에는 Configuration이라는 설정을 따로 만들어 그 클래스 내부에 @Bean으로 직접 빈으로 추가할 항목들을 넣고 이 속에서 직접 의존관계를 만들어주는 방식이다. 이는 처음에 빈을 등록할 때는 다소 귀찮음이 따르겠지만, 추후 변경을 원하는 경우 하나씩 다 수정해야하는 컴포넌트 스캔 방식과는 다르게 설정파일 속에 있는 코드만 바꾸면 되기에 변경을 자주 해야하는 상황에 쓰기 좋다.  

의존관계를 주입(DI)하는 방식에는 대략적으로 세가지가 존재한다.  
1.생성자 주입  
2.필드 주입  
3.Setter 주입  
가장 많이 쓰이는 것은 생성자 주입이고, Setter주입은 언뜻보면 생성자 주입과 비슷해보인다. 하지만 Setter함수 특성 상 코드를 public으로 지정해야하고, 이는 곧 다른 유저가 쉽게 코드에 영향을 줄 수 있는 것으로 보안의 취약성이 있기에 잘 사용하지 않는다.  

정형화된 코드에 있어서는 컴포넌트 스캔이 용이하다. 하지만 정형화가 되지 않았거나, 구현 클래스를 변경해야 하는 경우가 생기기 쉽다면 Configuration을 이용하여 직접 코드 등록을 하는 방식이 더욱 쓸모있을 것이다.  

스프링빈이 없다면 Autowired도 쓸모가 없다. 스프링 컨테이너에 빈이 등록되어 있는 것들 끌어오는 것이기에 당연한 것이다.