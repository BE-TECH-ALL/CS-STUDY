# Spring DI/IoC는 어떻게 동작하나요?
IoC(제어의 역전)은 프로그램의 제어 흐름을 직접 제어하는 것이 아니라 외부에서 관리하는 것으로 코드의 최종호출은 개발자가 제어하는 것이 아닌 프레임워크의 내부에서 결정된 대로 이루어집니다.
DI(의존관계 주입)은 Spring 프레임워크에서 지원하는 IoC의 형태로 클래스 사이의 의존관계를 빈 설정 정보를 바탕으로 컨테이너가 자동으로 연결해줍니다.
스프링에서는 스프링 컨테이너 ApplicationContext를 이용하여 설정 정보를 생성, 등록하고 필요한 객체를 생성자 혹은 setter를 통해 주입합니다.

# Spring Bean이란 무엇인가요?
스프링(Spring) 컨테이너가 관리하는 자바 객체를 빈(Bean)이라 합니다.
스프링의 특징에는 제어의 역전(IoC)이 있습니다.
제어의 역전이란, 간단히 말해서 객체의 생성 및 제어권을 사용자가 아닌 스프링에게 맡기는 것입니다.
IoC가 적용되지 않은 경우 사용자가 new연산을 통해 객체를 생성하고 메소드를 호출했습니다.
IoC가 적용된 경우에는 이러한 객체의 생성과 사용자의 제어권을 스프링에게 넘깁니다.
사용자는 직접 new를 이용해 생성한 객체를 사용하지 않고, 스프링에 의하여 관리당하는 자바 객체를 사용합니다. 이 객체를 ‘빈(bean)'이라고 합니다.

# 스프링 Bean의 생성 과정을 설명해주세요.
객체 생성 → 의존 설정 → 초기화 → 사용 → 소멸 과정의 생명주기를 가지고 있습니다. Bean은 스프링 컨테이너에 의해 생명주기를 관리하며 빈 초기화방법은 @PostConstruct 를 빈 소멸에서는 @PreDestroy 를 사용합니다.
생성한 스프링 빈을 등록할 때는 ComponentScan을 이용하거나 @Configuration 의 @Bean 을 사용하여 빈 설정파일에 직접 빈을 등록할 수 있습니다.

# 스프링 Bean의 Scope에 대해서 설명해주세요.
빈 스코프는 빈이 존재할 수 있는 범위를 뜻하며 싱글톤, 프로토타입, request, session, application 등이 있습니다.
싱글톤은 기본 스코프로 스프링 컨테이너의 시작과 종료까지 유지되는 가장 넓은 범위의 스코프입니다.
프로토타입은 빈의 생성과 의존관계 주입까지만 관여하고 더는 관리하지 않는 매우 짧은 범위의 스코프입니다.
request는 웹 요청이 들어오고 나갈때까지 유지하는 스코프, session은 웹 세션이 생성, 종료할때까지, application은 웹 서블릿 컨텍스트와 같은 범위로 유지하는 스코프입니다.

# DI 종류는 어떤것이 있고, 이들의 차이는 무엇인가요?
DI는 세가지 방법이 있습니다. 생성자 삽입, Setter를 이용한 메소드 매개 변수 삽입, 필드 주입이 있습니다.
생성자 주입은 생성자 호출시점에 딱 1번만 호출되는 것을 보장하며 불변, 필수 의존관계에 사용합니다.
Setter주입은 선택, 변경 가능성이 있는 의존관계에 사용되며 스프링빈을 선택적으로 등록이 가능합니다.
필드 주입은 `@Autowired` 를 사용하는데 외부에서 변경이 불가능하여 테스트 하기 힘듭니다. DI 프레임워크 없이는 작동하기 힘들며, 주로 애플리케이션과 관계없는 테스트코드나 `@Configuration` 같은 스프링 설정 목적으로 사용합니다.

# Bean/Component 어노테이션에 대해서 설명해주시고, 둘의 차이점에 대해 설명해주세요.
두 어노테이션 모두 IoC 컨테이너에 Bean을 등록하기 위해 사용합니다
@Component : 개발자가 작성한 class를 기반으로 실행시점에 인스턴스 객체를 1회(싱글톤) 생성합니다
@Controller, @Service, @Repository 는 모두 @Component 이며 실행시점에 자동으로 의존성을 주입합니다
@Bean : 개발자가 작성한 method를 기반으로 메서드에서 반환하는 객체를 인스턴스 객체로 1회(싱글톤) 생성합니다
