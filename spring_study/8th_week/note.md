# 8주차 내용정리  

## 섹션4  
### 스프링 컨테이너 생성  
스프링은 new AnnotationConfigApplicationContext를 통해 컨테이너가 생성된다.  
그 앞에 있는 ApplicationContext를 스프링 컨테이너라고 하는데 이는 인터페이스이다.  
스프링컨테이너는 XML기반으로도 만들 수 있고, 애노테이션 기반 자바 설정 클래스로 만들 수 있는데 요즘엔 거의 애노테이션 방식을 쓴다.  
new AnnotationConfigApplicationContext(AppConfig.class); 에서 보듯  
AppConfig를 매개변수로 하여 ApplicationContext의 구현체를 생성한 것이다.  
원래는 BeanFactory라는 최상위, 그 밑에 ApplicationContext로 구분되는데 빈팩토리는 거의 직접사용 안해서 ApplicationContext를 스프링 컨테이너라고 말하는 편이다.  
![img1](https://user-images.githubusercontent.com/108540812/218229218-b7b597c9-c3fc-4536-ad63-ad55d662686f.png)  
이후 빈을 등록한다. 빈의 이름은 항상 다른 이름을 부여해야한다. 완전 중요!!  
같은 이름을 불렀을 때, 기존 빈을 덮거나 다른 빈이 무시되거나 오류가 생기기 쉽다.  
이제 스프링빈을 등록하고 나서는 의존관계를 넣어준다. 이는 설정 정보를 참고한다.  
단순히 자바코드 같지만 차이가 있다고 한다. 뒤에 싱글톤 컨테이너에서 설명  
> 스프링은 빈생성, 의존관계주입 단계가 나눠져 있는데 우리가 한 것처럼 자바코드로 스프링 등록을 하면 생성자 호출하며 의존관계주입이 한번에 처리된다. 자동으로 의존관계가 연결되는 방식도 이후에 설명할 예정임

스프링 컨테이너에서 데이터를 조회하는 방법은 무엇일까  

### 스프링 컨테이너에 등록된 모든 빈 조회  
beanDefinitionNames라는 기능을 통해 스프링빈의 이름을 조회할 수 있는데, 이를 사용하면 스프링 내부의 빈과 직접 등록한 빈 모두 뜨는 것을 확인가능하다.  
따라서 Annotation...의 메소드 중 하나인 getBeanDefinitionNames를 통해 BeanDefinition 객체들을 만들어 놓고, 이들을 getRole()을 통해 ROLE_APPLICATION인지 ROLE_INFRASTRUCTURE인지 구분하여 원하는 빈을 조회할 수 있다.  

### 모두 조회 말고 기본적으로 스프링 빈 조회하는 방법  
스프링 컨테이너에서는 기본적으로 ac(AnnotationConfigApplicationContext).getBean("이름", 클래스명.class)을 사용하여 빈을 조회한다.  
이러한 검증은 assertThat(memberService).isInstanceOf(MemberServiceImpl.class);로 하였다.  
빈 이름으로 조회하지 못했을 때는 assertThrows를 사용하여 예외처리로 한다.  

### 동일한 타입이 둘 이상일 때 조회하는 방법  
getBean에서 타입만 지정했는데 MemberRepository 타입이 같은 것으로 2개라면  
getBean을 타입만으로 받지 말고 이름, 타입 둘다 받는 매개변수로 설정하면 된다.  
타입이 하나인데 여러개의 동일타입 빈이 들어오면 NoUniqueBeanDefinitionException이 발생한다.  

### 스프링 빈 조회 - 상속관계  
스프링 빈은 상속관계가 있는 경우 빈을 조회할 때 부모타입 아래에 있는 모든 자식타입이 같이 딸려온다.  
따라서, 모든 자바 객체의 부모인 Object 타입을 조회하면 모든 빈을 조회할 것이다.  
getBeansOfType을 통해 빈의 타입을 조회하는데 이 매개변수를 Object.class로 했더니 자바 내 모든 빈이 나타났다.  
빈을 조회할 일이 사실 실제론 별로 없는데 왜 해봤는지.  
부모타입으로 조회할 때 자식타입도 딸려온다는 것을 잘 이해시키기 위함이다.  

### BeanFactory, ApplicationContext  
전에 BeanFactory라고 최상위에 인터페이스가 있다고 했었다. 근데 잘 사용하지 않기에 사실상 ApplicationContext를 스프링 컨테이너라고 부른다 했다.  
그럼 과연 BeanFactory는 어떤 기능이 들어있을까  
우리가 지금까지 사용한 스프링의 기능들은 사실 BeanFactory내부에 있는 것들이다.  
예를들어 getBean같은 것들이 이에 해당된다.  
그러면 BeanFactory에서 이미 빈 조회 기능이 들어있는데 왜 ApplicationContext에서 불러올까?  
애플리케이션 개발엔 빈 관리, 조회도 중요한데 수 많은 부가기능이 필요로하다.  
ApplicatinContext는 BeanFactory도 받지만 그 외에도 여러가지의 부가 인터페이스들을 상속받고있다.  
메세지소스로 국제화기능, 환경변수, 애플리케이션이벤트, 편리한리소스조회...  
즉, ApplicationContext는 빈 관리 기능 + 부가기능 인 것이다.  

### XML로 설정하는 방법  
스프링 컨테이너는 유연하다. 다양한 형식의 설정 정보를 받아들일 수 있다.  
ApplicationContext를 AppConfig.class로 구현했었는데, 자바 코드가 아닌 xml로도 설정 정보로 구현할 수 있다. 임의로 구현도 가능  
즉, appconfig.xml의 형태도 가능하다는 것이다.  
그냥 new AnnotationConfigApplicationContext("AppConfig.class") 한 것 처럼 new GenericXmlApplicationContext("appConfig.xml)로 설정하면 된다.  
이후 xml파일을 생성해서 AppConfig.class를 설정했던 것 처럼 만든다.  
태그를 사용해서 bean을 등록하는 것과, 자바코드에서 @Bean을 사용한 것 둘 다 완벽히 똑같이 구현된다.  
xml기반이라 하더라도 인터페이스는 ApplicationContext를 상속받는다!  
빈이랑 똑같으니까 꼭 xml를 몰라도 된다. 스프링이 얼마나 유연한가를 보여주는 예시이다.  

### BeanDefinition은 무엇일까 - 스프링 빈 설정 메타정보  
스프링의 설정 형식의 중심에는 BeanDefinition이라는 추상화가 존재한다.  
스프링 컨테이너는 자바 코드인지, xml인지 상관 없고 오직 BeanDefinition만 알면 된다.  
스프링 컨테이너는 이 메타 정보를 기반으로 스프링 빈을 생성한다.  
역할과 구현을 개념적으로 나눈 것이다.  
ApplicationContext를 구현한 Annotation...Context는 DefinitionReader를 사용하여 설정 정보를 읽고 빈 메타정보를 생성해낸다.  
xml도 마찬가지, GenericXml...Context도 XmlBeanDefinitionReader가 존재한다. 이것이 설정 정보를 읽어 빈을 생성한다.  
beandefinition을 직접 생성하여 컨테이너에 등록할 수도 있는데 하지만 실무에서 이럴일은 거의 없다.  
그냥 BeanDefinition으로 추상화하여 스프링이 다양한 설정 정보를 사용한다는 것만 이해하면 된다.  
가끔 스프링코드나 오픈코드를 볼 때 BeanDefinition이라는 것이 보일 때가 있는데 위에서 말한 것처럼 이해하면 된다.(직접 등록하기도 함)  
테스트 코드에서 ApplicationContext로 안하고 그 하위 애들로 불러왔는데, ApplicationContext에는 getBeanDefinition기능은 없기 때문이다. 이는 실제로 쓸일 별로 없다는 걸 간접적으로 보여줌  
지금까진 빈을 직접 등록했는데 AppConfig 기능을 통해 직접 자바 코드를 넣고 연결시켜주는 방식을 팩토리메소드라고 한다.  
외부에서 메소드를 호출해서 생성하는 방식  

## 섹션5  
### 싱글톤
스프링은 그 목적이 기업에서 운영하는 온라인 서비스를 지원하는 것이다.  
그렇기에 스프링은 주로 웹 애플리케이션인데, 웹이 아닌 애플리케이션도 가능은 하다.  
웹 애플리케이션의 특징은 여러 고객이 동시에 요청을 한다는 것이다.  
지금껏 만든 AppConfig는 요청을 받을 때마다 새로운 객체를 생성함  
초당 1000명의 고객이 요청하면 초당 1000개의 객체를 생성하고 소멸해야한다.  
이는 메모리의 낭비로 이어진다. 그렇기에 해당 객체가 딱 1개 생성되고 이것이 공유되도록 하는 해결 방안이 있다. 이것을 싱글톤 패턴이라 부른다  
클래스의 인스턴스가 1개만 생성되는 디자인. 따라서 2개 이상 생성 안되도록 막아야한다.  
private 생성자를 통해 외부에서 임의로 생성하지 못하도록 방지  
인스턴스는 여러개지만 참조하는 값은 같은 객체를 참조하는 것이다.  
하지만 싱글톤 패턴의 문제점도 있으니..  
> 싱글톤 패턴 구현에 코드가 복잡해진다.  
클라이언트가 구체 클래스에 의존하게 되어 DIP를 위반한다.  
DIP를 위반하기에 OCP를 위반하기 쉽다.  
내부 속성 변경이 어렵고 유연성이 떨어진다.  
private 생성자이기에 자식 클래스를 만들기 어렵다.  
안티패턴이라고도 불린다.

이런 싱글톤패턴의 문제점을 해결하고자 스프링 컨테이너를 사용하여 싱글톤컨테이너를 구현할 수 있던 것이다.  
스프링 컨테이너는 싱글턴 패턴을 안써도 객체 인스턴스를 1개로 관리한다. (싱글톤)  
스프링 컨테이너의 이런 기능을 싱글톤 레지스트리 라고 부른다.  
싱글톤 때문에 지저분하게 코드를 적지 않아도 되고 DIP와 OCP위반 걱정을 하지 않아도 되고 private로 부터 자유로워진다.  
클라이언트가 서비스를 요청하면 스프링 컨테이너에 등록된 빈이 동일한 서비스를 반환하는 것이기에 여러 객체를 생성해야하는 기존의 모습과 상반된다.  
물론 요청할 때마다 새로운 객체를 생성하여 반환하는 기능도 있긴하다. 추후 설명  
싱글톤 방식을 사용하기 위해서는 싱글톤 객체의 상태를 의존적인 필드가 없도록, 특정 클라이언트 값을 변경하지 않도록, 가급적 읽기모드이도록 영향을 끼치지 않는 형태로 만들어야 한다.  
공유필드다 보니 조심!!! 스프링 빈은 항상 무상태(stateless)가 중요  

### Configuration은..?  
중복되면 안된다했는데 우리가 만들었던 Configuration에는 memberRepository 메소드가 두번 호출되는 상황이 보인다. (MemberService와 OrderService)  
실제로 이를 검증하여 테스트해보면 분명 여러번 호출하였음에도 출력 결과는 1번만 출력되는 것을 볼 수 있다.  
분명 코드 상엔 여러번 출력되어야 하는데 왜 그럴까?  
사실 이것은 @Configuration을 통해 스프링이 내부적으로 CGLIB라는 바이트 조작 라이브러리를 사용하기 때문이다.  
AppConfig클래스가 순수 AppConfig클래스로 존재하지 않고, AppConfig를 상속받은 임의의 다른 클래스 AppConfig@CGLIB를 만들어 등록하기에 이 CGLIB가 싱글톤이 되도록 해준다.  
아마 이 라이브러리의 내부엔 이미 빈이 컨테이너에 등록이 되어있으면 반환하는 형식의 로직이 들어있으리라 예상할 수 있다.  
그러면 @Configuration을 사용하지 않으면 여러번 호출하면 여러번 출력될까?  
바로 정답이다.  
즉, 요약하면 @Bean만 사용해도 스프링 컨테이너에 등록하는데에는 문제가 없다.  
하지만 우리는 싱글톤을 보장하기 위하여 설정 정보에 @Configuration을 사용해야 한다.  
