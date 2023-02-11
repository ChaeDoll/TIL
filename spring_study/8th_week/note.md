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

### 

## 섹션5