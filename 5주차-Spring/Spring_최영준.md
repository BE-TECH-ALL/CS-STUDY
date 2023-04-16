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
- IoC 컨테이너는 먼저 Bean 클래스의 인스턴스를 생성합니다. 이를 위해 Java Reflection API를 사용하여 클래스를 로드하고 객체를 생성합니다.

2. 의존성 주입(Dependency Injection)
- Bean의 생성자, Setter 메서드, 필드 등을 통해 Bean 객체가 의존하는 다른 객체를 주입합니다. IoC 컨테이너에서 관리되는 다른 Bean 객체를 주입하는 것이 일반적입니다.

3. 초기화 및 소멸 메서드 호출
- Bean 객체가 생성되고, 의존성이 주입된 후에는 초기화 메서드와 소멸 메서드를 호출합니다. 초기화 메서드는 Bean 객체가 사용될 준비가 완료된 후에 호출되고 소멸 메서드는 Bean 객체가 사용되지 않게 될 때 호출됩니다.

- 객체 생성 → 의존 설정 → 초기화 → 사용 → 소멸 과정

Bean은 스프링 컨테이너에 의해 생명주기를 관리하며 빈 초기화방법은 @PostConstruct 를 빈 소멸에서는 @PreDestroy 를 사용합니다.
생성한 스프링 빈을 등록할 때는 ComponentScan을 이용하거나 @Configuration 의 @Bean 을 사용하여 빈 설정파일에 직접 빈을 등록할 수 있습니다.

## 스프링 Bean의 Scope에 대해서 설명해주세요.
빈 스코프는 빈이 존재할 수 있는 범위를 뜻하며 싱글톤, 프로토타입, request, session, application 등이 있습니다.

1. Singleton
- Singleton은 Spring에서 가장 기본적인 Scope이며 Bean이 하나의 인스턴스만 생성되도록 합니다. 따라서 애플리케이션 전체에서 하나의 인스턴스를 공유하며 이를 통해 메모리 사용을 최소화할 수 있습니다. 기본값으로 Singleton이 설정되어 있습니다.

2. Prototype
- Prototype은 Bean을 요청할 때마다 새로운 인스턴스를 생성하도록 합니다. 따라서 Singleton과 달리 매번 새로운 인스턴스가 생성되므로, 메모리 사용량이 증가할 수 있습니다.

3. Request
- Request Scope는 Spring MVC 웹 애플리케이션에서 사용됩니다. 각각의 HTTP 요청마다 새로운 인스턴스를 생성하도록 하며 요청이 끝날 때 Bean 객체가 소멸됩니다.

4. Session
- Session Scope는 Spring MVC 웹 애플리케이션에서 사용됩니다. 각각의 세션마다 새로운 인스턴스를 생성하도록 하며 세션이 끝날 때 Bean 객체가 소멸됩니다.

5. GlobalSession
- GlobalSession Scope는 Spring MVC 웹 애플리케이션에서 사용됩니다. Portlet 환경에서 사용되며 모든 포틀릿에서 하나의 인스턴스를 공유하도록 합니다.

## IoC 컨테이너의 역할은 무엇이 있을까요?
1. 객체의 생성과 관리
- IoC 컨테이너는 Bean이라고 불리는 객체를 생성하고 관리합니다. 이를 통해 개발자는 객체의 생성 및 관리에 대한 부분에서 벗어나 Bean의 라이프사이클과 의존성 주입 등을 Spring Framework에게 맡길 수 있습니다.

2. 의존성 주입(Dependency Injection)
- IoC 컨테이너는 Bean이 의존하는 다른 Bean 객체를 주입합니다. 이를 통해 개발자는 Bean의 의존성을 외부에서 주입받게 되어 객체 간의 결합도를 낮출 수 있습니다.

3. 객체의 스코프 관리
- IoC 컨테이너는 Bean의 스코프를 관리합니다. Singleton, Prototype, Request, Session, GlobalSession 등 다양한 스코프를 지원하며, Bean의 스코프를 지정하여 라이프사이클을 관리할 수 있습니다.

4. AOP(Aspect Oriented Programming) 지원
- IoC 컨테이너는 AOP를 지원하여 애플리케이션에서 발생하는 여러 문제를 해결할 수 있습니다. 예를 들어 로깅, 보안, 트랜잭션 등의 공통적인 기능을 모듈화하여 여러 Bean에서 공통적으로 사용할 수 있습니다.

5. 다국어 지원
- IoC 컨테이너는 메시지 리소스(Message Resources)를 지원하여 다국어 애플리케이션을 개발할 수 있습니다. 이를 통해 개발자는 메시지 번들(Message Bundle)을 생성하고 이를 애플리케이션에서 사용할 수 있습니다.

6. 통합 및 확장성
- IoC 컨테이너는 다양한 플랫폼 및 기술과 통합할 수 있습니다. 예를 들어 JDBC, Hibernate, JPA 등과 같은 데이터 액세스 기술과 통합하여 사용할 수 있으며, 개발자는 이러한 기술을 활용하여 애플리케이션을 개발할 수 있습니다.

## DI 종류는 어떤것이 있고, 이들의 차이는 무엇인가요?
1. Constructor Injection (생성자 주입)
- Constructor Injection은 생성자를 통해 의존성을 주입하는 방법입니다. 생성자 파라미터의 타입에 맞는 Bean 객체를 주입합니다.
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
- Setter Injection은 Setter 메서드를 통해 의존성을 주입하는 방법입니다. Setter 메서드 파라미터의 타입에 맞는 Bean 객체를 주입합니다.

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
- Field Injection은 필드에 직접 의존성을 주입하는 방법입니다. Spring에서는 필드에 @Autowired 어노테이션을 붙여서 사용하며 필드의 타입에 맞는 Bean 객체를 주입합니다.

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
- Spring IoC 컨테이너에서는 Bean 객체를 생성합니다. Bean 객체는 XML 설정 파일, Java Annotation 등을 통해 등록되어 있어야 합니다.

2. 의존성 검색
- Spring IoC 컨테이너는 Bean 객체가 의존하는 다른 Bean 객체를 검색합니다. 이때, 의존성은 @Autowired, @Inject, @Resource 등의 어노테이션을 통해 설정될 수 있습니다.

3. 의존성 주입
- Spring IoC 컨테이너는 검색된 Bean 객체를 해당 필드, 생성자, Setter 메서드 등을 통해 주입합니다. 이때, 필드에 @Autowired, 생성자에 @Autowired, @Inject, Setter 메서드에 @Autowired, @Inject, @Resource 등의 어노테이션을 붙여서 사용합니다.

4. Bean 객체 초기화
- 의존성이 모두 주입된 Bean 객체는 초기화됩니다. 이때, 초기화 메서드(@PostConstruct 어노테이션을 붙인 메서드)가 있다면, 해당 메서드가 호출됩니다.

5. Bean 객체 사용
- 의존성이 모두 주입되어 초기화된 Bean 객체는 애플리케이션에서 사용됩니다.

## Spring Web MVC의 Dispatcher Servlet의 동작 원리에 대해서 간단히 설명해주세요.
1. 클라이언트 요청(Request) 처리:
- 클라이언트가 요청한 URL 정보를 토대로 Dispatcher Servlet이 요청(Request)을 처리합니다.

2. Handler Mapping
- 요청(Request) 정보를 분석하여 적절한 컨트롤러(Controller)를 찾기 위해 Handler Mapping을 수행합니다. Handler Mapping은 요청(Request) 정보를 분석하여 적절한 컨트롤러(Controller)를 결정합니다.

3. Controller 호출
- Handler Mapping을 통해 결정된 컨트롤러(Controller)를 호출합니다.

4. Controller 처리
- 컨트롤러(Controller)는 요청(Request)을 처리한 후, Model과 View 정보를 반환합니다.

5. View Resolver
- Model과 View 정보를 토대로 적절한 View를 결정하기 위해 View Resolver를 수행합니다. View Resolver는 Model과 View 정보를 분석하여 적절한 View를 결정합니다.

6. View 처리
- View Resolver를 통해 결정된 View를 호출하여 요청(Request)에 대한 결과를 생성합니다.

7. 클라이언트 응답(Response) 처리:
- 생성된 응답(Response)을 클라이언트에게 전달합니다.


![dispatcher servlet](https://user-images.githubusercontent.com/97837003/232323795-67d79b82-cdfd-44e8-bb9e-aabc89f60ac8.png)


## 프론트 컨트롤러 패턴이란 무엇인가요?
프론트 컨트롤러 패턴(Front Controller Pattern)은 웹 애플리케이션에서 모든 요청(Request)을 중앙 집중적으로 처리하는 디자인 패턴입니다.

- 프론트 컨트롤러의 구조
  - 프론트 컨트롤러(Front Controller):
    - 모든 요청(Request)을 받아서 처리할 컨트롤러(Controller)를 결정하고, 각 컨트롤러가 공통으로 처리해야 하는 로직을 처리합니다.

  - 컨트롤러(Controller):
    - 각 요청(Request)에 대해 처리해야 하는 로직을 구현합니다.

  - 뷰(View):
    - 컨트롤러(Controller)에서 생성된 결과를 보여줄 View를 결정합니다.

- 프론트 컨트롤러 패턴의 장점
  - 중앙 집중적인 요청 처리
    - 프론트 컨트롤러를 통해 모든 요청(Request)을 중앙 집중적으로 처리할 수 있으므로 요청 처리의 일관성과 효율성을 높일 수 있습니다.

  - 공통 로직 처리
    - 프론트 컨트롤러에서 공통으로 처리해야 하는 로직을 구현할 수 있으므로 각 컨트롤러(Controller)에서 중복되는 코드를 줄일 수 있습니다.

  - 유연한 뷰(View) 선택
    - 프론트 컨트롤러를 통해 뷰(View)를 선택할 수 있으므로 컨트롤러(Controller)에서 뷰(View)를 선택하는 것보다 유연하게 뷰(View)를 선택할 수 있습니다.

- 프론트 컨트롤러 패턴의 단점
  - 복잡한 구조
    - 프론트 컨트롤러 패턴은 구조가 복잡하여 개발 초기 단계에서는 구조를 설계하는 데 시간이 걸릴 수 있습니다.

  - 성능 문제
    - 프론트 컨트롤러는 모든 요청(Request)을 처리하므로 처리 시간이 길어질 수 있습니다. 따라서, 성능에 대한 고려가 필요합니다.


## Servlet Filter와 Spring Interceptor의 차이는 무엇인가요?
Servlet Filter와 Spring Interceptor는 모두 웹 애플리케이션에서 클라이언트 요청(Request)에 대한 전처리(pre-processing)와 후처리(post-processing)를 수행하는 기능을 제공합니다. 

Filter는 Method Signature에 있는 Argument인 HttpServletRequest 혹은 HttpServeltResponse를 ServletRequest, ServletResponse 등으로 교체할 때 사용하거나, 데이터 변환(다운로드 파일의 압축 및 데이터 암호화 등), XSL/T를 이용한 XML 문서 변경, 사용자 인증, 자원 접근에 대한 로깅 등에 사용합니다.

Interceptor의 경우 AOP를 흉내내거나, Spring 애플리케이션에서 전역적으로 전후처리 로직에서 예외를 사용하도록 하거나, Handler Method에서 사용자의 권한을 체크해서 다른 동작을 시켜준다거나 할 때 사용합니다.

- 두 방식의 차이점
1. 실행 시점
  - Servlet Filter는 클라이언트 요청(Request)을 처리하기 전과 후에 실행됩니다. 반면, Spring Interceptor는 클라이언트 요청(Request)을 처리하기 전, 컨트롤러(Controller) 실행 전, 컨트롤러(Controller) 실행 후, 뷰(View) 생성 전, 뷰(View) 렌더링 후 등 여러 시점에서 실행될 수 있습니다.

2. 처리 대상
  - Servlet Filter는 모든 요청(Request)에 대해 처리할 수 있습니다. 반면, Spring Interceptor는 Dispatcher Servlet이 처리하는 요청(Request)에 대해서만 처리할 수 있습니다.

3. 구현 방식
  - Servlet Filter는 Servlet API를 사용하여 구현됩니다. 반면, Spring Interceptor는 Spring Framework에서 제공하는 HandlerInterceptor 인터페이스를 구현하여 구현됩니다.

4. 컨트롤러(Controller) 접근
  - Servlet Filter는 컨트롤러(Controller)에 직접 접근할 수 없습니다. 반면, Spring Interceptor는 컨트롤러(Controller)에 접근하여 요청(Request) 처리 결과를 수정할 수 있습니다.

5. 응답(Response) 처리
  - Servlet Filter는 응답(Response)에 대한 처리를 수행할 수 있습니다. 반면, Spring Interceptor는 컨트롤러(Controller) 실행 후, 뷰(View) 생성 전 등 여러 시점에서 응답(Response)에 대한 처리를 수행할 수 있습니다.

6. Spring Framework과의 연동
  - Servlet Filter는 Servlet API를 사용하여 구현되므로, Spring Framework과의 연동이 어렵습니다. 반면, Spring Interceptor는 Spring Framework에서 제공하는 기능이므로, Spring Framework과의 연동이 용이합니다.

## Spring에서 CORS 에러를 해결하기 위한 방법을 설명해주세요.
CORS(Cross-Origin Resource Sharing)는 웹 브라우저에서 보안상의 이유로 다른 도메인(Origin)에서 리소스에 접근할 때 발생하는 보안 정책입니다.

1. @CrossOrigin 어노테이션 사용
- Spring에서는 @CrossOrigin 어노테이션을 사용하여 CORS 에러를 해결할 수 있습니다. 이 어노테이션을 사용하면, 해당 컨트롤러(Controller)의 모든 핸들러(Handler)에서 CORS를 허용할 수 있습니다. 
```
@RestController
@CrossOrigin(origins = "http://localhost:3000")
public class UserController {
    // 컨트롤러 핸들러 메서드
}
```

2. WebMvcConfigurer를 구현하여 설정
Spring에서는 WebMvcConfigurer 인터페이스를 구현하여 CORS 설정을 할 수도 있습니다. 이를 통해 보다 세밀한 설정이 가능합니다. 
```
@Configuration
public class CorsConfiguration implements WebMvcConfigurer {
 
    @Override
    public void addCorsMappings(CorsRegistry registry) {
        registry.addMapping("/**")
                .allowedOrigins("http://localhost:3000")
                .allowedMethods("GET", "POST", "PUT", "DELETE")
                .allowedHeaders("*");
    }
}
```


3. Filter를 이용한 설정:
Spring에서는 Filter를 이용하여 CORS 설정을 할 수도 있습니다. 이 방법은 WebMvcConfigurer를 구현하는 방법과 유사하지만, 보다 세부적인 설정이 가능합니다. 
```
@Component
@Order(Ordered.HIGHEST_PRECEDENCE)
public class CorsFilter implements Filter {

    @Override
    public void doFilter(ServletRequest req, ServletResponse res, FilterChain chain) throws IOException, ServletException {
        HttpServletResponse response = (HttpServletResponse) res;
        HttpServletRequest request = (HttpServletRequest) req;

        response.setHeader("Access-Control-Allow-Origin", "http://localhost:3000");
        response.setHeader("Access-Control-Allow-Methods", "POST, GET, OPTIONS, DELETE, PUT");
        response.setHeader("Access-Control-Allow-Headers", "*");
        response.setHeader("Access-Control-Allow-Credentials", "true");

        if ("OPTIONS".equalsIgnoreCase(request.getMethod())) {
            response.setStatus(HttpServletResponse.SC_OK);
        } else {
            chain.doFilter(req, res);
        }
    }
}
```

## Bean/Component 어노테이션에 대해서 설명해주시고, 둘의 차이점에 대해 설명해주세요.
@Bean 어노테이션과 @Component 어노테이션은 Spring에서 Bean으로 등록하기 위해 사용되는 어노테이션입니다.

@Bean 어노테이션은 Java Config에서 사용되며 개발자가 직접 작성한 method를 기반으로 메서드에서 반환하는 객체를 인스턴스 객체로 1회(싱글톤) 생성합니다

@Component 어노테이션은 클래스에 사용되며 Spring에서 Bean으로 등록될 수 있도록 합니다. @Controller, @Service, @Repository 는 모두 @Component 이며 실행시점에 자동으로 의존성을 주입합니다

1. 사용 방법
- @Bean 어노테이션은 Java Config에서 사용되며 개발자가 직접 설정 클래스를 작성하여 Bean을 등록합니다. 반면, @Component 어노테이션은 클래스에 직접 사용되며 Spring이 자동으로 Bean으로 등록합니다.

2. 등록 대상
- @Bean 어노테이션은 메서드에 사용되며 해당 메서드가 반환하는 객체를 Bean으로 등록합니다. 반면, @Component 어노테이션은 클래스에 사용되며, 해당 클래스를 Bean으로 등록합니다.

3. Bean 이름
- @Bean 어노테이션은 Bean의 이름을 지정할 수 있습니다. 반면, @Component 어노테이션은 클래스 이름을 기반으로 Bean의 이름을 자동으로 생성합니다.

4. 범위
- @Bean 어노테이션은 Bean의 범위(Scope)을 지정할 수 있습니다. 반면, @Component 어노테이션은 Bean의 범위(Scope)를 지정할 수 없습니다.

## POJO란 무엇인가요? Spring Framework에서 POJO는 무엇이 될 수 있을까요?
POJO(Plain Old Java Object)는 프레임워크 인터페이스, 클래스를 구현하거나 확장하지 않은 단순한 클래스로 Java에서 제공하는 API 외에 종속되지 않습니다. 

특정 환경에 종속되지 않아 코드가 간결하고 테스트 자동화에 유리합니다. 스프링에서는 도메인과 비즈니스 로직을 수행하는 대상이 POJO대상이 될 수 있습니다.

## Spring Web MVC에서 요청 마다 Thread가 생성되어 Controller를 통해 요청을 수행할텐데, 어떻게 1개의 Controller만 생성될 수 있을까요?
생성한 Controller 클래스에 대한 정보가 JVM 메모리 영역 중 Method Area(메서드 영역)에 올라가기 때문입니다. Controller 객체는 Heap(힙)에 생성 되지만, 해당 클래스의 정보(메소드 처리 로직, 명령들)는 Method Area(메서드 영역)에 생성 됩니다. 따라서 결국 모든 Thread가 객체의 메서드를 공유할 수 있기 때문에 Controller는 1개만 생성됩니다.

각각의 Thread는 singleton으로 생성된 Bean( ⇒ Controller 포함 ) 들을 참고하여 일을 합니다. Bean들은 기본적으로 Singleton으로 생성되고 관리되는데, 사실상 이 Thread들은 그 1개의 Singleton Controller 객체를 공유하기에 최종적으로 1개의 Controller만 사용합니다. 즉, 하나의 Singleton Controller가 수많은 request를 처리한다기 보다는, 각각의 Thread가 singleton으로 생성된 Controller를 참고하여 실행한다고 보면 됩니다.

원래 동기화를 해주는 이유는 프로세스(Thread)들간 알고있는 정보(상태)를 일치하기 위해서인데, Controller가 내부적으로 상태를 갖는 것이 없으니, 그냥 메소드 호출만 하면 됩니다. (공유하는 데이터 즉, 클래스변수, 전역변수를 컨트롤러에서 사용하지 않기 때문에 상태를 갖는 것이 없음)
그로 인해 굳이 동기화할 이유도 없고 그저 처리 로직만 ‘공유되어’ 사용됩니다. 따라서 스레드는 Controller의 메소드를 공유하고 제각각 호출할 수 있기 때문에 들어오는 요청이 1만 개의 요청이든 10만 개의 요청이든 처리할 수 있습니다.

## Filter는 Servlet의 스펙이고, Interceptor는 Spring MVC의 스펙입니다. Spring Application에서 Filter와 Interceptor를 통해 예외를 처리할 경우 어떻게 해야 할까요?
동작 대상이 다르기 때문에 필터는 예외가 발생하면 Web Application에서 처리해야 합니다. 선언이나 필터 내에서 request.getRequestDispatcher(String)과 같이 예외 처리 할 수 있습니다.
반면 인터셉터는 스프링의 ServletDispatcher내부에 있으므로 @ConstrollerAdvice에서 @ExceptionHandler를 사용해 예외처리 할 수 있습니다.

## Spring Application을 구동할 때 메서드를 실행시키는 방법에 대해 설명해주세요.
1. InitializingBean과 DisposableBean 인터페이스 구현
- InitializingBean과 DisposableBean 인터페이스를 구현한 클래스에서는 각각의 인터페이스 메서드인 afterPropertiesSet()과 destroy()가 호출됩니다. 이를 통해 객체 생성 시 초기화 작업이 필요한 경우, afterPropertiesSet() 메서드에서 해당 작업을 수행할 수 있습니다. 또한, 객체 소멸 시 정리 작업이 필요한 경우, destroy() 메서드에서 해당 작업을 수행할 수 있습니다.
```
public class MyBean implements InitializingBean, DisposableBean {

    @Override
    public void afterPropertiesSet() throws Exception {
        // 객체 생성 시 초기화 작업 수행
    }

    @Override
    public void destroy() throws Exception {
        // 객체 소멸 시 정리 작업 수행
    }
}
```

2. @PostConstruct와 @PreDestroy 어노테이션 사용
- @PostConstruct와 @PreDestroy 어노테이션을 사용하여 객체 생성 시 초기화 작업과 객체 소멸 시 정리 작업을 수행할 수 있습니다.
```
public class MyBean {

    @PostConstruct
    public void init() {
        // 객체 생성 시 초기화 작업 수행
    }

    @PreDestroy
    public void cleanUp() {
        // 객체 소멸 시 정리 작업 수행
    }
}
```

3. @Bean 어노테이션과 initMethod와 destroyMethod 속성 사용
- @Bean 어노테이션에서 initMethod와 destroyMethod 속성을 사용하여 객체 생성 시 초기화 작업과 객체 소멸 시 정리 작업을 수행할 수 있습니다.
```
@Configuration
public class AppConfig {

    @Bean(initMethod = "init", destroyMethod = "cleanUp")
    public MyBean myBean() {
        return new MyBean();
    }
}
```

## 의존성과 설정값을 생성자 인자로 주입해야 하는 이유에 대해 설명해주세요.
1. 객체의 불변성 확보
- 실제로 개발을 하다 보면 의존 관계의 변경이 필요한 상황은 거의 없다. 하지만 수정자 주입이나 일반 메소드 주입을 이용하면 불필요하게 수정의 가능성을 열어두어 유지보수성을 떨어뜨린다. 그러므로 생성자 주입을 통해 변경의 가능성을 배제하고 불변성을 보장하는 것이 좋다.

2. 테스트 코드의 작성
- 테스트가 특정 프레임워크에 의존하는 것은 침투적이므로 좋지 못하다. 그러므로 가능한 순수 자바로 테스트를 작성하는 것이 가장 좋은데, 생성자 주입이 아닌 다른 주입으로 작성된 코드는 순수한 자바 코드로 단위 테스트를 작성하는 것이 어렵다. 생성자 주입을 사용하면 컴파일 시점에 객체를 주입받아 테스트 코드를 작성할 수 있으며, 주입하는 객체가 누락된 경우 컴파일 시점에 오류를 발견할 수 있다. 심지어 우리가 테스트를 위해 만든 Test객체를 생성자로 넣어 편리함을 얻을 수도 있다.

3. final 키워드 작성 및 Lombok과의 결합
- 생성자 주입을 사용하면 필드 객체에 final 키워드를 사용할 수 있으며, 컴파일 시점에 누락된 의존성을 확인할 수 있다. 반면에 다른 주입 방법들은 객체의 생성(생성자 호출) 이후에 호출되므로 final 키워드를 사용할 수 없다. 또한 final 키워드를 붙이면 Lombok과 결합되어 코드를 간결하게 작성할 수 있다.

4. 스프링에 비침투적인 코드 작성
- 필드 주입을 사용하려면 @Autowired를 이용해야 하는데, 이것은 스프링이 제공하는 어노테이션이다. 그러므로 @Autowired를 사용하면 스프링 의존성이 침투하게 된다. 

5. 순환 참조 에러 방지
- 생성자 주입을 사용하면 애플리케이션 구동 시점(객체의 생성 시점)에 순환 참조 에러를 예방할 수 있다.

참고 - https://mangkyu.tistory.com/125

# JPA

## JPA 영속성 컨텍스트의 이점(5가지)을 설명해주세요.
1. 1차 캐시(First Level Cache)
- 1차 캐시는 엔티티를 메모리 상에 저장하여, 같은 엔티티가 다시 조회될 때는 데이터베이스에 접근하지 않고 1차 캐시에서 엔티티를 반환합니다. 이를 통해 성능을 향상시킬 수 있습니다.

2. 지연 로딩(Lazy Loading)
- 지연 로딩은 연관된 엔티티를 실제로 사용할 때만 로딩하는 기법입니다. 이를 통해 데이터베이스에 대한 부하를 줄일 수 있습니다.

3. Dirty Checking
- JPA 영속성 컨텍스트는 엔티티의 상태 변화를 감지하여 자동으로 데이터베이스에 반영합니다. 이를 Dirty Checking이라고 합니다. Dirty Checking을 사용하면 개발자가 직접 데이터베이스에 반영하는 코드를 작성할 필요가 없습니다.

4. 트랜잭션 쓰기 지연(Transaction Write-behind)
- 트랜잭션 쓰기 지연은 트랜잭션이 커밋될 때까지 엔티티의 상태를 변경한 후, 일괄적으로 데이터베이스에 반영하는 기법입니다. 이를 통해 데이터베이스에 대한 부하를 줄일 수 있습니다.

5. 쓰기 지연(SQL Batch)
- 쓰기 지연은 일괄적인 SQL 쿼리를 배치로 처리하여 데이터베이스에 대한 부하를 줄이는 기법입니다. 이를 통해 성능을 향상시킬 수 있습니다.

## JPA Propagation 전파단계를 설명해주세요.
1. REQUIRED
- 현재 실행중인 트랜잭션이 존재하면 해당 트랜잭션을 사용하고, 그렇지 않으면 새로운 트랜잭션을 시작합니다. REQUIRED 전파 속성은 일반적으로 트랜잭션의 기본값입니다.

2. SUPPORTS
- 현재 실행중인 트랜잭션이 존재하면 해당 트랜잭션을 사용하고, 그렇지 않으면 트랜잭션 없이 메서드를 실행합니다.

3. MANDATORY
- 현재 실행중인 트랜잭션이 존재하면 해당 트랜잭션을 사용하고, 그렇지 않으면 예외를 발생시킵니다.

4. REQUIRES_NEW
- 항상 새로운 트랜잭션을 시작합니다. 현재 실행중인 트랜잭션이 있으면 해당 트랜잭션을 일시 중지하고, 새로운 트랜잭션을 시작합니다.

5. NOT_SUPPORTED
- 현재 실행중인 트랜잭션을 일시 중지하고, 트랜잭션 없이 메서드를 실행합니다.

6. NEVER
- 현재 실행중인 트랜잭션이 있으면 예외를 발생시키고, 그렇지 않으면 트랜잭션 없이 메서드를 실행합니다.

7. NESTED
- 현재 실행중인 트랜잭션이 있으면 그 트랜잭션 안에 중첩된 트랜잭션을 시작합니다. 중첩된 트랜잭션은 독립적인 커밋 및 롤백을 수행할 수 있습니다.

## JPA를 쓴다면 그 이유에 대해서 설명해주세요.
JPA는 JPQL로 SQL을 추상화하기 때문에 RDBMS Vendor에 관계없이 동일한 쿼리를 작성해서 같은 동작을 기대할 수 있다는 장점도 가지고 있습니다. 이는 database dialect를 지원하기 때문에 가지는 장점입니다.

제가 JPA를 사용하는 이유는 객체지향 프레임워크이기 때문입니다. JPA를 사용하면 비즈니스 로직이 RDBMS에 의존하는 것이 아니라, 자바 코드로 표현될 수 있기 때문입니다. 그로 인해서 생산성이 높아진다고 볼 수 있습니다.

## N + 1 문제는 무엇이고 이것이 발생하는 이유와 이를 해결하는 방법을 설명해주세요.
N + 1 쿼리 문제는 즉시 로딩과 지연 로딩 전략 각각의 상황에서 발생할 수 있습니다. 하위 엔티티들이 존재하는 경우 한 쿼리에서 모두 가져오는 것이 아닌, 필요한 곳에서 각각 쿼리가 발생하는 경우를 이릅니다.

즉시 로딩에서 발생하는 이유는 JPQL을 사용하는 경우 전체 조회를 했을 때, 영속성 컨텍스트가 아닌 데이터베이스에서 직접 데이터를 조회한 다음 즉시로딩 전략이 동작하기 때문입니다.

지연 로딩에서 발생하는 이유는 지연로딩 전략을 사용한 하위 엔티티를 로드할 때, JPA에서 프록시 엔티티를 unproxy 할 때 해당 엔티티를 조회하기 위한 추가적인 쿼리가 실행되어 발생합니다.

해결 방법으로는 Fetch Join이라고 불리는 JPQL의 join fetch를 사용하는 방법이 있으며, 또 다른 방법으로는 @EntityGraph를 사용하는 방법, @Fetch(FetchMode.SUBSELECT)를 사용하는 방법, @BatchSize를 사용해 조절하거나 전역적인 batch-size를 설정하는 방법이 있습니다.
