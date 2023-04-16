# Spring

## Spring DI/IoC는 어떻게 동작하나요?
Spring의 DI (Dependency Injection) 또는 IoC (Inversion of Control)은 객체 간의 의존성을 관리하는 방법입니다.

DI는 객체 간의 의존성을 더 이상 코드 내부에서 생성하거나 관리하지 않고 외부에서 주입하도록 만드는 디자인 패턴입니다. 이렇게 하면 코드가 더 유연하고 확장 가능해지며 유닛 테스트가 용이해집니다. Spring에서는 DI를 위해 Bean이라고 불리는 객체를 생성하고 이를 IoC 컨테이너에 등록하여 관리합니다.

IoC는 객체의 생성과 관리를 개발자가 하는 것이 아니라 Spring Framework가 대신 수행하는 것을 말합니다. 이를 통해 개발자는 객체를 생성하고 객체 간의 의존성을 관리하는 복잡한 작업에서 벗어날 수 있습니다. 대신 Spring Framework가 객체의 라이프사이클과 의존성 주입을 담당하게 됩니다.

Spring에서 IoC는 ApplicationContext라는 인터페이스를 구현하는 BeanFactory를 통해 구현됩니다. 개발자가 BeanFactory에 필요한 Bean들을 등록하면 BeanFactory는 이를 관리하고, 필요한 시점에 필요한 Bean을 제공합니다. 이를 통해 객체 간의 의존성이 외부에서 주입되기 때문에 코드의 유지보수성이 향상되고 확장성이 좋아집니다.

## Spring Bean이란 무엇인가요?
Spring Framework에서 Bean은 Spring IoC 컨테이너에 의해 생성되고 관리되는 객체를 말합니다. Spring에서 Bean은 IoC 컨테이너에 등록되어 필요할 때마다 IoC 컨테이너에서 생성되고 관리됩니다.

Bean은 일반적으로 애플리케이션에서 많이 사용되는 객체를 말하는데, DAO(Data Access Object)나 Service 객체 등이 Bean으로 등록됩니다. Bean은 기본적으로 싱글톤(Singleton)으로 생성되기 때문에 애플리케이션 전체에서 공유되어 사용됩니다.

Spring에서 Bean은 일반적으로 Java 클래스로 표현됩니다. Spring에서는 이러한 클래스들을 Bean으로 등록하고, 이를 IoC 컨테이너에 등록하여 관리합니다. 이를 통해 개발자는 객체 생성과 관리에 대한 부분에서 벗어나, Bean의 라이프사이클과 의존성 주입 등을 Spring Framework에게 맡길 수 있습니다.

Spring에서는 Bean을 등록하는 방법으로 XML, Java Annotation, Java Config 등이 있습니다.

## 스프링 Bean의 생성 과정을 설명해주세요.
1. Bean의 인스턴스화
IoC 컨테이너는 먼저 Bean 클래스의 인스턴스를 생성합니다. 이를 위해 Java Reflection API를 사용하여 클래스를 로드하고 객체를 생성합니다.

2. 의존성 주입(Dependency Injection)
Bean의 생성자, Setter 메서드, 필드 등을 통해 Bean 객체가 의존하는 다른 객체를 주입합니다. IoC 컨테이너에서 관리되는 다른 Bean 객체를 주입하는 것이 일반적입니다.

3. 초기화 및 소멸 메서드 호출
Bean 객체가 생성되고, 의존성이 주입된 후에는 초기화 메서드와 소멸 메서드를 호출합니다. 초기화 메서드는 Bean 객체가 사용될 준비가 완료된 후에 호출되고 소멸 메서드는 Bean 객체가 사용되지 않게 될 때 호출됩니다.

- 객체 생성 → 의존 설정 → 초기화 → 사용 → 소멸 과정

Bean은 스프링 컨테이너에 의해 생명주기를 관리하며 빈 초기화방법은 @PostConstruct 를 빈 소멸에서는 @PreDestroy 를 사용합니다.
생성한 스프링 빈을 등록할 때는 ComponentScan을 이용하거나 @Configuration 의 @Bean 을 사용하여 빈 설정파일에 직접 빈을 등록할 수 있습니다.

## 스프링 Bean의 Scope에 대해서 설명해주세요.
빈 스코프는 빈이 존재할 수 있는 범위를 뜻하며 싱글톤, 프로토타입, request, session, application 등이 있습니다.

1. Singleton
Singleton은 Spring에서 가장 기본적인 Scope이며 Bean이 하나의 인스턴스만 생성되도록 합니다. 따라서 애플리케이션 전체에서 하나의 인스턴스를 공유하며 이를 통해 메모리 사용을 최소화할 수 있습니다. 기본값으로 Singleton이 설정되어 있습니다.

2. Prototype
Prototype은 Bean을 요청할 때마다 새로운 인스턴스를 생성하도록 합니다. 따라서 Singleton과 달리 매번 새로운 인스턴스가 생성되므로, 메모리 사용량이 증가할 수 있습니다.

3. Request
Request Scope는 Spring MVC 웹 애플리케이션에서 사용됩니다. 각각의 HTTP 요청마다 새로운 인스턴스를 생성하도록 하며 요청이 끝날 때 Bean 객체가 소멸됩니다.

4. Session
Session Scope는 Spring MVC 웹 애플리케이션에서 사용됩니다. 각각의 세션마다 새로운 인스턴스를 생성하도록 하며 세션이 끝날 때 Bean 객체가 소멸됩니다.

5. GlobalSession
GlobalSession Scope는 Spring MVC 웹 애플리케이션에서 사용됩니다. Portlet 환경에서 사용되며 모든 포틀릿에서 하나의 인스턴스를 공유하도록 합니다.

## IoC 컨테이너의 역할은 무엇이 있을까요?
1. 객체의 생성과 관리
IoC 컨테이너는 Bean이라고 불리는 객체를 생성하고 관리합니다. 이를 통해 개발자는 객체의 생성 및 관리에 대한 부분에서 벗어나 Bean의 라이프사이클과 의존성 주입 등을 Spring Framework에게 맡길 수 있습니다.

2. 의존성 주입(Dependency Injection)
IoC 컨테이너는 Bean이 의존하는 다른 Bean 객체를 주입합니다. 이를 통해 개발자는 Bean의 의존성을 외부에서 주입받게 되어 객체 간의 결합도를 낮출 수 있습니다.

3. 객체의 스코프 관리
IoC 컨테이너는 Bean의 스코프를 관리합니다. Singleton, Prototype, Request, Session, GlobalSession 등 다양한 스코프를 지원하며, Bean의 스코프를 지정하여 라이프사이클을 관리할 수 있습니다.

4. AOP(Aspect Oriented Programming) 지원
IoC 컨테이너는 AOP를 지원하여 애플리케이션에서 발생하는 여러 문제를 해결할 수 있습니다. 예를 들어 로깅, 보안, 트랜잭션 등의 공통적인 기능을 모듈화하여 여러 Bean에서 공통적으로 사용할 수 있습니다.

5. 다국어 지원
IoC 컨테이너는 메시지 리소스(Message Resources)를 지원하여 다국어 애플리케이션을 개발할 수 있습니다. 이를 통해 개발자는 메시지 번들(Message Bundle)을 생성하고 이를 애플리케이션에서 사용할 수 있습니다.

6. 통합 및 확장성
IoC 컨테이너는 다양한 플랫폼 및 기술과 통합할 수 있습니다. 예를 들어 JDBC, Hibernate, JPA 등과 같은 데이터 액세스 기술과 통합하여 사용할 수 있으며, 개발자는 이러한 기술을 활용하여 애플리케이션을 개발할 수 있습니다.

## DI 종류는 어떤것이 있고, 이들의 차이는 무엇인가요?
1. Constructor Injection (생성자 주입)
Constructor Injection은 생성자를 통해 의존성을 주입하는 방법입니다. 생성자 파라미터의 타입에 맞는 Bean 객체를 주입합니다.
```
public class Car {
  private Engine engine;
  
  public Car(Engine engine) { // 
    this.engine = engine;
  }
  
  public void start() {
    engine.start();
    System.out.println("Car is started.");
  }
}
```
- lombok을 사용하는 경우

```
@RequiredArgsConstructor
public class Car {
  private final Engine engine;
  
  public void start() {
    engine.start();
    System.out.println("Car is started.");
  }
}
```


2. Setter Injection (Setter 이용)
Setter Injection은 Setter 메서드를 통해 의존성을 주입하는 방법입니다. Setter 메서드 파라미터의 타입에 맞는 Bean 객체를 주입합니다.

```
public class Car {
  private Engine engine;
  
  public void setEngine(Engine engine) { // set 메소드 이용
    this.engine = engine;
  }
  
  public void start() {
    engine.start();
    System.out.println("Car is started.");
  }
}
```


3. Field Injection (필드 주입)
Field Injection은 필드에 직접 의존성을 주입하는 방법입니다. Spring에서는 필드에 @Autowired 어노테이션을 붙여서 사용하며 필드의 타입에 맞는 Bean 객체를 주입합니다.

```
public class Car {
  @Autowired // 어노테이션 사용
  private Engine engine;
  
  public void start() {
    engine.start();
    System.out.println("Car is started.");
  }
}
```

- 세 가지 방법의 차이점
  - 생성자 주입: 생성자 호출 시점에 딱 1번만 호출되는 것을 보장하며, 불변, 필수 의존관계에 사용
  - Setter 주입: 선택, 변경 가능성이 있는 의존관계에 사용되며 스프링빈을 선택적으로 등록이 가능
  - 필드 주입: '@Autowired'를 사용하는데 외부에서 변경이 불가능하여 테스트 하기 힘듬. DI 프레임워크 없이는 작동하기 힘들며, 주로 애플리케이션과 관계 없는 테스트 코드나  '@Configuration' 같은 스프링 설정 목적으로 사용

## Autowiring 과정에 대해서 설명해주세요.
Autowiring은 Spring Framework에서 Bean 객체의 의존성을 자동으로 주입하는 기능을 말합니다.

1. Bean 객체 생성
Spring IoC 컨테이너에서는 Bean 객체를 생성합니다. Bean 객체는 XML 설정 파일, Java Annotation 등을 통해 등록되어 있어야 합니다.

2. 의존성 검색
Spring IoC 컨테이너는 Bean 객체가 의존하는 다른 Bean 객체를 검색합니다. 이때, 의존성은 @Autowired, @Inject, @Resource 등의 어노테이션을 통해 설정될 수 있습니다.

3. 의존성 주입
Spring IoC 컨테이너는 검색된 Bean 객체를 해당 필드, 생성자, Setter 메서드 등을 통해 주입합니다. 이때, 필드에 @Autowired, 생성자에 @Autowired, @Inject, Setter 메서드에 @Autowired, @Inject, @Resource 등의 어노테이션을 붙여서 사용합니다.

4. Bean 객체 초기화
의존성이 모두 주입된 Bean 객체는 초기화됩니다. 이때, 초기화 메서드(@PostConstruct 어노테이션을 붙인 메서드)가 있다면, 해당 메서드가 호출됩니다.

5. Bean 객체 사용
의존성이 모두 주입되어 초기화된 Bean 객체는 애플리케이션에서 사용됩니다.

## Spring Web MVC의 Dispatcher Servlet의 동작 원리에 대해서 간단히 설명해주세요.
1. 클라이언트 요청(Request) 처리:
클라이언트가 요청한 URL 정보를 토대로 Dispatcher Servlet이 요청(Request)을 처리합니다.

2. Handler Mapping
요청(Request) 정보를 분석하여 적절한 컨트롤러(Controller)를 찾기 위해 Handler Mapping을 수행합니다. Handler Mapping은 요청(Request) 정보를 분석하여 적절한 컨트롤러(Controller)를 결정합니다.

3. Controller 호출
Handler Mapping을 통해 결정된 컨트롤러(Controller)를 호출합니다.

4. Controller 처리
컨트롤러(Controller)는 요청(Request)을 처리한 후, Model과 View 정보를 반환합니다.

5. View Resolver
Model과 View 정보를 토대로 적절한 View를 결정하기 위해 View Resolver를 수행합니다. View Resolver는 Model과 View 정보를 분석하여 적절한 View를 결정합니다.

6. View 처리
View Resolver를 통해 결정된 View를 호출하여 요청(Request)에 대한 결과를 생성합니다.

클라이언트 응답(Response) 처리:
생성된 응답(Response)을 클라이언트에게 전달합니다.

## 프론트 컨트롤러 패턴이란 무엇인가요?

## Servlet Filter와 Spring Interceptor의 차이는 무엇인가요?

## Spring에서 CORS 에러를 해결하기 위한 방법을 설명해주세요.

## Bean/Component 어노테이션에 대해서 설명해주시고, 둘의 차이점에 대해 설명해주세요.

## POJO란 무엇인가요? Spring Framework에서 POJO는 무엇이 될 수 있을까요?

## Spring Web MVC에서 요청 마다 Thread가 생성되어 Controller를 통해 요청을 수행할텐데, 어떻게 1개의 Controller만 생성될 수 있을까요?

## Filter는 Servlet의 스펙이고, Interceptor는 Spring MVC의 스펙입니다. Spring Application에서 Filter와 Interceptor를 통해 예외를 처리할 경우 어떻게 해야 할까요?

## Spring Application을 구동할 때 메서드를 실행시키는 방법에 대해 설명해주세요.

## 의존성과 설정값을 생성자 인자로 주입해야 하는 이유에 대해 설명해주세요.

## 싱글톤 패턴에 대해서 설명해주세요.



# JPA

## JPA 영속성 컨텍스트의 이점(5가지)을 설명해주세요.

## JPA Propagation 전파단계를 설명해주세요.

## JPA를 쓴다면 그 이유에 대해서 설명해주세요.

## N + 1 문제는 무엇이고 이것이 발생하는 이유와 이를 해결하는 방법을 설명해주세요.
