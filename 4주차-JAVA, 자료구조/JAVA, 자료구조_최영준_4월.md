# JAVA

## JVM의 구조와 Java의 실행방식을 설명해주세요.
JVM은 Java Virtual Machine이란 뜻으로, Java 언어로 작성된 프로그램을 실행하기 위한 가상 머신입니다. Java는 컴파일된 바이트 코드를 JVM에 전달하고, JVM은 이 바이트 코드를 기계어로 번역하고 실행합니다. JVM의 구조는 Class Loader, Execution engine, Runtime Data Area, JNI, Native Method Library로 이루어져 있습니다.

- Class Loader : JVM내로 클래스를 로드하고, 링크를 통해 배치하는 작업을 수행하는 모듈입니다. Java 클래스 파일은 JVM에서 실행하기 전에 먼저 로딩되어야 합니다.
- Execution engine : 바이트 코드를 실행시키는 역할을 합니다.
  - 인터프리터: 바이트 코드를 한줄 씩 실행합니다.
  - JIT 컴파일러: 인터피르터 효율을 높이기 위한 컴파일러로 인터프리터가 반복되는 코드를 발견하면 JIT 컴파일러가 반복되는 코드를 네이티브 코드로 바꿔줍니다. 그 다음부터 인터프리터는 네이티브 코드로 컴파일된 코드를 바로 사용합니다.
  - GC(Garbage Collector) : 가비지 컬렉터로 힙 영역에서 사용되지 않는 객체들을 제거하는 작업을 의미합니다.
- Runtime Data Areas: 프로그램 실행 중에 사용되는 다양한 영역입니다.
  - PC Register : Thread가 시작될 때 생성되며 현재 수행 중인 JVM 명령의 주소를 갖고 있습니다.
  - Stack Area : 지역 변수, 파라미터 등이 생성되는 영역. 실제 객체는 Heap에 할당되고 해당 레퍼런스만 Stack에 저장됩니다.
  - Heap Area : 동적으로 생성된 오브젝트와 배열이 저장되는 곳으로 GC의 대상 영역입니다.
  - Method Area : 클래스 멤버 변수, 메소드 정보, Type 정보, Constant Pool, static, final 변수 등이 생성됩니다. 상수 풀(Constant Pool)은 모든 Symbolic Reference를 포함하고 있습니다.
- JNI(Java Native Interface) : 자바 애플리케이션에서 C, C++, 어셈블리어로 작성된 함수를 사용할 수 있는 방법을 제공해줍니다. Native 키워드를 사용하여 메서드를 호출합니다. 대표적인 메서드는 Thread의 currentThread()입니다.
- Native Method Library : C, C++로 작성된 라이브러리 입니다.

Java의 실행방식
- 소스 코드 작성: Java 언어로 작성된 소스 코드를 작성합니다.

- 컴파일: Java 컴파일러(javac)를 사용하여 소스 코드를 바이트 코드로 변환합니다.

- 로딩: 클래스 로더가 바이트 코드를 로딩하여 Runtime Data Area의 Method Area에 저장합니다.

- 링크: 런타임 상수 풀(Constant Pool)이나 다른 클래스에 대한 참조를 해석하고, 필요한 메모리를 할당합니다.

- 초기화: 클래스 변수(static 변수)와 클래스 메서드(static method)를 위한 메모리를 할당하고 초기화합니다.

- 실행: Execution Engine이 바이트 코드를 해석하고 실행합니다.

- 종료: 프로그램이 종료되면 JVM은 할당된 메모리를 회수하고 종료됩니다.

## GC가 무엇인지, 필요한 이유는 무엇인지, 동작방식에 대해 설명해주세요.
GC(Garbage Collection)는 자바에서 메모리를 관리하는 프로세스 중 하나입니다. GC는 동적으로 할당된 메모리 중에서 더 이상 사용하지 않는 객체를 찾아 제거하고, 메모리를 회수하는 작업을 수행합니다.

GC가 필요한 이유
- 메모리 누수 방지: 객체를 생성하고 사용하는 동안에 메모리를 할당하게 됩니다. 그러나 객체를 사용하지 않더라도 메모리는 계속해서 사용되고 있어서 시스템의 메모리 사용량이 증가하게 됩니다. GC는 이러한 불필요한 메모리 사용을 감지하여 회수함으로써 메모리 누수를 방지합니다.

- 메모리 할당 최적화: 메모리 할당과 회수는 언제든 일어날 수 있으므로 시스템의 성능에 큰 영향을 미칩니다. GC는 메모리 할당과 회수를 최적화하여 시스템 성능을 개선합니다.

GC의 동작방식
- 객체 추적: GC는 Heap 영역에서 사용 중인 객체들을 추적합니다. 객체가 더 이상 사용되지 않을 때, 즉 참조하는 변수가 없을 때 해당 객체는 가비지(Garbage)로 간주됩니다.

- 가비지 식별: GC는 가비지인 객체들을 식별합니다. 가비지는 Heap 영역에서 다른 객체들과 구분됩니다.

- 가비지 수집: GC는 가비지인 객체들을 수집하여 메모리를 회수합니다. 수집된 객체는 Heap 영역에서 해제됩니다.

- 메모리 정리: 가비지 수집 후, GC는 Heap 영역에서 메모리 조각을 정리하고, 다시 사용 가능한 상태로 만듭니다.

## 컬렉션 프레임워크에 대해서 설명해주세요.
컬렉션 프레임워크(Collection Framework)는 자바에서 데이터를 저장하고 처리하기 위한 인터페이스와 클래스의 모음입니다. 컬렉션 프레임워크는 다양한 자료구조를 제공하며, 이를 활용하여 데이터를 보다 쉽게 다룰 수 있습니다.

컬렉션 프레임워크의 주요 인터페이스
- List 인터페이스: 순서가 있는 데이터 집합을 다루는 인터페이스로, 데이터를 인덱스로 접근할 수 있습니다. ArrayList, LinkedList 등이 List 인터페이스를 구현합니다.

- Set 인터페이스: 순서가 없는 데이터 집합을 다루는 인터페이스로, 중복된 값을 허용하지 않습니다. HashSet, TreeSet 등이 Set 인터페이스를 구현합니다.

- Map 인터페이스: Key-Value 쌍으로 데이터를 저장하고 다루는 인터페이스로, Key를 이용하여 Value를 검색합니다. HashMap, TreeMap 등이 Map 인터페이스를 구현합니다.

컬렉션 프레임워크의 장점

- 자료구조의 추상화: 컬렉션 프레임워크는 다양한 자료구조를 제공하므로, 데이터를 다루는 방식에 따라 적합한 자료구조를 선택하여 사용할 수 있습니다.

- 유연한 데이터 처리: 컬렉션 프레임워크는 다양한 메서드를 제공하므로, 데이터를 보다 쉽게 처리할 수 있습니다. 예를 들어, List 인터페이스는 데이터를 인덱스로 접근할 수 있는 메서드와, 데이터를 검색하는 메서드 등을 제공합니다.

- 표준화된 인터페이스: 컬렉션 프레임워크는 인터페이스와 구현 클래스를 분리하여, 다른 구현 클래스로 쉽게 대체할 수 있도록 구현되어 있습니다. 이로 인해 코드의 재사용성과 유지보수성이 높아집니다.

- 메모리와 성능 최적화: 컬렉션 프레임워크는 내부적으로 데이터를 저장하고 처리하기 위해 알고리즘을 사용합니다. 이 알고리즘은 메모리와 성능을 최적화하는 방향으로 구현되어 있습니다.

## 제네릭에 대해서 설명해주세요.
제네릭(Generic)은 자바에서 데이터 타입을 일반화하는 기능을 제공합니다. 제네릭은 컴파일 시점에 타입 안정성을 보장하므로, 프로그래밍의 실수를 줄이고 유지보수성을 높여줍니다.

## 애노테이션에 대해서 설명해주세요.
애노테이션(Annotation)은 자바에서 소스 코드에 메타데이터를 추가하기 위한 방법입니다. 애노테이션은 컴파일러나 런타임 시점에 소스 코드에 대한 정보를 제공하며, 코드의 문서화와 유지보수를 보다 쉽게 할 수 있습니다. 애노테이션은 컴파일 시점과 런타임 시점에 활용될 수 있으며, 애노테이션을 이용하여 자바 소스 코드의 가독성과 유지보수성을 높일 수 있습니다.

## 오버라이딩과 오버로딩이 무엇이며 어떤 차이가 있을까요?
오버라이딩(Overriding): 상위 클래스에서 정의된 메서드를 하위 클래스에서 재정의하는 것을 말합니다. 오버라이딩된 메서드는 상위 클래스의 메서드와 같은 이름, 매개변수, 반환 타입을 가져야 합니다. 하위 클래스에서 오버라이딩한 메서드는 상위 클래스에서 정의된 동일한 메서드를 가리키며, 이를 런타임 다형성이라고 합니다.

오버로딩(Overloading): 같은 이름의 메서드를 여러 개 정의하는 것을 말합니다. 메서드의 시그니처(매개변수의 개수, 타입, 순서)가 다르면 서로 다른 메서드로 인식합니다. 즉, 같은 이름의 메서드이지만 매개변수의 타입이나 개수 등이 다른 경우, 서로 다른 메서드로 처리됩니다.

오버로딩과 오버라이딩은 메서드의 다형성을 구현하는 데 사용되며, 서로 다른 개념입니다. 오버로딩은 같은 이름의 메서드를 여러 개 정의하는 것을 말하며, 오버라이딩은 상위 클래스의 메서드를 하위 클래스에서 재정의하는 것을 말합니다.

@Override 애노테이션을 써줘야 하는 이유
- 코드 가독성 향상: @Override 애노테이션을 사용하면, 코드의 가독성이 향상됩니다. 이 애노테이션을 사용하면, 오버라이딩된 메서드임을 명시적으로 나타낼 수 있으므로, 코드를 이해하는 데 도움을 줍니다.

- 실수 방지: @Override 애노테이션을 사용하면, 오버라이딩된 메서드를 잘못 구현하는 실수를 방지할 수 있습니다. 만약 오버라이딩된 메서드를 잘못 구현하면, 컴파일러가 오류를 발생시키기 때문입니다.

- 컴파일러 경고 방지: 만약 @Override 애노테이션을 사용하지 않고, 오버라이딩된 메서드를 잘못 구현하면, 컴파일러가 경고를 발생시킵니다. 이러한 경고는 코드의 오류를 발견하는 데 도움이 되지만, @Override 애노테이션을 사용하면, 이러한 경고를 방지할 수 있습니다.

## 인터페이스와 추상클래스의 차이점에 대해 설명해주세요.
인터페이스와 추상클래스는 자바에서 추상화를 구현하는 두 가지 방법입니다. 여기서 추상화는 구현 세부 정보를 숨기고 추상적인 개념만을 다루는 것을 말합니다.
- 인터페이스(Interface): 인터페이스는 추상적인 개념을 정의하는데 사용됩니다. 인터페이스는 메서드의 시그니처만을 정의하고, 메서드의 구현은 인터페이스를 구현하는 클래스에서 수행합니다. 즉, 인터페이스는 일종의 계약(contract)으로, 해당 인터페이스를 구현하는 클래스는 정의된 메서드를 반드시 구현해야 합니다.
- 추상클래스(Abstract Class): 추상클래스는 인터페이스와 비슷하게 추상화를 구현하는데 사용됩니다. 추상클래스는 일부 메서드를 구현할 수 있으며, 구현되지 않은 메서드를 추상 메서드로 정의할 수 있습니다. 추상 메서드는 인터페이스와 마찬가지로 구현되지 않은 메서드를 정의하는데 사용됩니다.

인터페이스와 추상클래스의 차이점
- 메서드 구현 여부: 인터페이스는 메서드의 구현을 하지 않으며, 추상클래스는 메서드의 일부를 구현할 수 있습니다.

- 다중 상속 가능 여부: 자바에서는 클래스의 다중 상속이 불가능합니다. 하지만, 인터페이스는 다중 상속이 가능합니다. 즉, 여러 개의 인터페이스를 구현할 수 있습니다.

## 클래스는 무엇이고 객체는 무엇인가요?
클래스(Class)는 자바에서 객체(Object)를 생성하기 위한 설계도 또는 틀을 말합니다. 클래스는 객체의 속성을 정의하고, 객체가 수행할 수 있는 행위를 정의하는 메서드를 포함합니다. 객체는 이러한 클래스를 바탕으로 생성됩니다.

객체(Object)는 클래스(Class)를 기반으로 생성된 실체(Instance)를 말합니다. 즉, 클래스는 객체를 생성하기 위한 설계도일 뿐, 객체는 이 설계도를 바탕으로 생성된 실체입니다. 객체는 클래스에서 정의된 속성과 메서드를 포함하며, 이를 이용하여 프로그램에서 데이터를 처리하고 조작합니다.

예를 들어, 자동차 클래스를 생성한다면, 이 클래스는 자동차 객체를 생성하기 위한 설계도가 됩니다. 자동차 객체는 클래스에서 정의된 속성(차종, 모델, 색상 등)과 메서드(주행, 정비, 가속 등)를 포함하며, 이를 이용하여 자동차를 운전하고 관리할 수 있습니다.

자바에서는 클래스를 이용하여 객체를 생성하며, 객체는 프로그램에서 데이터를 처리하고 조작하는데 사용됩니다. 따라서, 객체는 클래스의 실체로서 중요한 역할을 합니다.

## 정적(static)이란 무엇인가요?
Java에서 static 키워드를 사용하면, 해당 클래스의 정적 변수와 정적 메서드는 프로그램이 실행될 때 메모리에 딱 한 번만 할당되며, 객체 생성 없이 클래스 이름으로 접근할 수 있습니다.
정적 변수와 정적 메서드는 메모리 상에 클래스 정보(Method Area)에 저장됩니다. 클래스가 로드될 때 클래스 정보가 메모리에 할당되며, 해당 클래스의 정적 변수와 정적 메서드도 함께 할당됩니다. 이후 프로그램이 실행되는 동안, 해당 클래스의 정적 변수와 정적 메서드는 프로그램 전체에서 공유되며, 객체 생성 없이도 클래스 이름으로 접근할 수 있습니다.

그러나, GC의 관리 영역 밖에 존재하기 때문에 프로그램 종료시까지 메모리가 할당된 채로 존재합니다. 너무 남발하게 되면 시스템 성능에 악영향을 줄 수 있습니다.

- 정적 변수(Static variable): 클래스 변수라고도 하며, 클래스와 관련된 공통된 속성을 가지고 있는 변수입니다. 정적 변수는 객체 생성 없이도 클래스 이름으로 접근할 수 있습니다. 또한, 정적 변수는 프로그램이 실행되는 동안 메모리에서 유지되며, 모든 객체에서 공유됩니다.

- 정적 메서드(Static method): 클래스와 관련된 메서드로, 객체 생성 없이도 클래스 이름으로 접근할 수 있습니다. 정적 메서드는 클래스의 상태에 의존하지 않는 메서드로, 객체를 생성하지 않고도 호출할 수 있습니다.

## 자바의 원시타입들은 무엇이 있으며 각각 몇 바이트를 차지하나요?
자바에서 사용되는 원시 데이터 타입(Primitive data types) 종류
- byte : 1 byte, -128 ~ 127 범위의 부호 있는 정수를 저장할 수 있습니다.
- short : 2 bytes, -32,768 ~ 32,767 범위의 부호 있는 정수를 저장할 수 있습니다.
- int : 4 bytes, -2,147,483,648 ~ 2,147,483,647 범위의 부호 있는 정수를 저장할 수 있습니다.
- long : 8 bytes, -9,223,372,036,854,775,808 ~ 9,223,372,036,854,775,807 범위의 부호 있는 정수를 저장할 수 있습니다.
- float : 4 bytes, 소수점 이하 7자리까지 정확도를 가진 부동 소수점 수를 저장할 수 있습니다.
- double : 8 bytes, 소수점 이하 15자리까지 정확도를 가진 부동 소수점 수를 저장할 수 있습니다.
- char : 2 bytes, 유니코드 문자 하나를 저장할 수 있습니다.
- boolean : 1 byte (1 bit로도 가능하지만, 실제로는 1 byte로 할당), true 또는 false 값을 저장할 수 있습니다.

## 접근 제어자의 종류와 이에 대해 설명해주세요.
- public: 어떤 패키지에서도 접근이 가능합니다. public으로 선언된 멤버는 다른 패키지에서도 접근할 수 있습니다.

- protected: 같은 패키지에서는 물론 자식 클래스에서도 접근이 가능합니다. protected로 선언된 멤버는 같은 패키지의 다른 클래스나 자식 클래스에서 접근할 수 있습니다.

- default (package-private): 접근 제어자를 지정하지 않은 경우, 같은 패키지에서만 접근이 가능합니다. default로 선언된 멤버는 같은 패키지의 다른 클래스에서는 접근할 수 있지만, 다른 패키지에서는 접근할 수 없습니다.

- private: 같은 클래스에서만 접근이 가능합니다. private으로 선언된 멤버는 해당 클래스 내부에서만 접근할 수 있습니다.

## 객체지향에 대해서 설명해주세요.
객체지향은 의존성 관리입니다. 객체지향으로 의존성을 관리함으로써 변경 영향을 최소화하고 독립적인 배포가 가능해지며 독립적인 개발이 가능해집니다. 

객체지향의 특징
- 캡슐화(Encapsulation): 객체의 내부 데이터와 메서드를 외부에서 접근할 수 없도록 보호하는 기능입니다. 캡슐화를 통해 객체의 내부 구현을 숨기고, 객체와 객체 간의 인터페이스를 정의하여 더욱 안정적인 프로그래밍을 가능하게 합니다.

- 상속(Inheritance): 부모 클래스의 특징을 자식 클래스에서 상속받아 사용하는 기능입니다. 상속을 통해 코드의 재사용성을 높일 수 있으며, 클래스 간의 관계를 명확하게 표현할 수 있습니다.

- 다형성(Polymorphism): 같은 이름의 메서드나 연산자가 다양한 방식으로 동작하는 기능입니다. 다형성을 통해 객체의 유연한 동작을 가능하게 하며, 코드의 가독성을 높이고 유지보수를 용이하게 합니다.

## SOLID(객체지향 5대원칙)에 대해서 설명해주세요
- SRP (Single Responsibility Principle) 단일 책임 원칙: 모든 클래스는 하나의 책임만 가져야 합니다. 클래스가 담당하는 책임이 많아지면 코드의 응집도가 낮아지고, 유지보수와 확장이 어려워집니다.
  - ex : UI 컴포넌트의 렌더링과 데이터 로딩을 담당하는 코드를 분리하여, 각각의 클래스에서 하나의 책임만을 가지도록 설계한다. 

- OCP (Open/Closed Principle) 개방-폐쇄 원칙: 소프트웨어 개체(클래스, 모듈, 함수 등)는 확장에 대해 개방적이어야 하고, 변경에 대해서는 폐쇄적이어야 합니다. 즉, 코드 수정 없이 확장이 가능해야 합니다.
  - ex : 새로운 기능을 추가할 때, 기존의 코드를 수정하지 않고 새로운 클래스를 만들어서 확장성을 높이도록 설계한다.  

- LSP (Liskov Substitution Principle) 리스코프 치환 원칙: 상위 클래스는 하위 클래스에 대해 치환 가능해야 합니다. 이를 통해 상위 클래스와 하위 클래스 간의 인터페이스 일관성을 유지하고, 하위 클래스에서 상위 클래스의 기능을 오버라이딩하여 다형성을 지원할 수 있습니다.
  - ex : 상위 클래스와 하위 클래스 간에는 기능에 대한 일관성이 있어야 하며, 하위 클래스에서 상위 클래스의 메서드를 오버라이드할 때는 메서드의 사전 조건과 사후 조건을 유지해야 한다.
  
- ISP (Interface Segregation Principle) 인터페이스 분리 원칙: 인터페이스는 클라이언트가 필요로 하는 기능에 대해서만 제공해야 합니다. 즉, 인터페이스는 작고 응집도 높은 단위로 분리되어야 하며, 클라이언트는 자신이 필요한 인터페이스만 사용해야 합니다.
  - ex : 인터페이스를 구현할 때, 해당 인터페이스에서 사용하지 않는 메서드를 구현하지 않도록 하여, 인터페이스의 응집도를 높이고, 클라이언트가 사용하지 않는 기능에 대한 의존성을 낮춘다. 

- DIP (Dependency Inversion Principle) 의존 역전 원칙: 고수준 모듈은 저수준 모듈에 의존하면 안 되며, 추상화에 의존해야 합니다. 즉, 의존성 주입을 통해 모듈 간의 의존성을 낮추고, 코드의 재사용성과 확장성을 높여야 합니다.
  - ex : 상위 수준의 클래스에서 하위 수준의 클래스를 직접 생성하거나 의존하는 것이 아니라, 인터페이스를 통해 의존성을 주입받도록 설계하여, 모듈 간의 결합도를 낮추고, 유연성을 높인다.

## 동일성(identity)와 동등성(equality)에 대해 설명해주세요. (equals(), ==)
- 동일성(identity)은 두 객체가 완전히 동일한 객체인지를 비교하는 것입니다. 두 객체가 동일하다는 것은 객체의 메모리 상의 주소 값이 같다는 것을 의미합니다. 이를 확인하기 위해서는 == 연산자를 사용합니다.

- 동등성(equality)은 두 객체가 내용이 같은지를 비교하는 것입니다. 두 객체가 동등하다는 것은 객체의 내용이 같다는 것을 의미합니다. 이를 확인하기 위해서는 equals() 메서드를 사용합니다.

예를들어,
```
String str1 = "Hello";
String str2 = new String("Hello");
```
- 위의 코드에서 str1과 str2는 모두 "Hello"라는 문자열을 저장하고 있습니다. 하지만 str1과 str2는 서로 다른 객체입니다. str1은 상수 풀(constant pool)에서 가져온 문자열을 참조하고 있지만, str2는 새로운 객체를 생성하여 문자열을 저장하고 있기 때문입니다. 따라서 str1과 str2는 동등한 내용을 가지고 있지만, 동일한 객체가 아니므로, str1 == str2는 false를 반환합니다. 반면에 str1.equals(str2)는 true를 반환합니다.

## 원시타입과 참조타입의 차이에 대해 설명해주세요.
- 원시 타입 : 논리형(boolean), 문자형(char), 정수형(byte, short, int, long), 실수형(float, double)의 총 8개로 이루어져 있습니다. 이러한 원시 타입의 변수는 실제 값(value) 자체를 저장합니다. 예를 들어, int 타입의 변수에 10을 할당하면, 변수는 10이라는 값을 직접 저장합니다.

- 참조 타입 : 객체(object)의 주소(reference)를 저장합니다. 객체는 클래스(class)를 통해 정의되며, 객체는 클래스의 인스턴스(instance)입니다. 참조 타입의 변수는 객체의 주소를 저장하므로, 실제 값은 객체가 저장하고 있는 데이터(data)입니다. 예를 들어, String 타입의 변수에 "Hello"를 할당하면, 변수는 문자열 "Hello"를 저장하는 객체의 주소를 가리키게 됩니다.

원시 타입과 참조 타입의 가장 큰 차이점은 변수가 저장하는 값의 종류입니다. 원시 타입은 값 자체를 저장하며, 참조 타입은 객체의 주소를 저장합니다.

## String, StringBuilder, StringBuffer 각각의 차이에 대해 설명해주세요.
- String
  - 불변(immutable) 클래스
  - 문자열을 수정하면 새로운 문자열 객체를 생성하여 참조
  - 멀티스레드 환경에서 안전
  - 문자열 연산이 빈번하지 않을 때 사용하는 것이 좋음
 
- StringBuilder
  - 가변(mutable) 클래스
  - 문자열을 직접 수정
  - 멀티스레드 환경에서는 안전하지 않음
  - 문자열 연산이 빈번할 때 사용하는 것이 좋음 
  
- StringBuffer
  - 가변(mutable) 클래스
  - 문자열을 직접 수정
  - 멀티스레드 환경에서 안전
  - 문자열 연산이 빈번하고, 동기화(synchronization)가 필요할 때 사용하는 것이 좋음
 
 문자열 연산이 빈번하고 동기화가 필요한 경우에는 StringBuffer를 사용하고, 그렇지 않은 경우에는 StringBuilder를 사용하는 것이 좋습니다. String은 문자열을 수정할 일이 없거나, 문자열 연산이 빈번하지 않을 때 사용하는 것이 좋습니다.

## Checked Exception과 Unchecked Exception에 대해 설명해주세요. 스프링 트랜잭션 추상화에서 rollback 대상은 무엇일까요?
Checked Exception은 RuntimeException을 제외한 모든 예외 클래스의 상위 클래스인 Exception 클래스를 상속받은 예외입니다. Checked Exception은 컴파일러가 예외 처리를 강제하는 예외이며, 반드시 예외 처리를 해주어야 합니다.

Unchecked Exception은 RuntimeException 클래스를 상속받은 예외입니다. Unchecked Exception은 컴파일러가 예외 처리를 강제하지 않으며, 예외 처리를 하지 않아도 컴파일이 가능합니다.

Spring 트랜잭션 추상화에서 rollback 대상은 RuntimeException과 Error입니다. 즉, Unchecked Exception이나 그 하위 클래스인 RuntimeException 예외가 발생하면 자동으로 롤백됩니다. 이는 예기치 않은 상황에서 트랜잭션을 롤백하는 것이 좋기 때문입니다. Checked Exception은 트랜잭션 롤백 대상이 아니며, 직접 예외 처리를 해주어야 합니다.

## Java8에서 추가된 기능에 대해서 설명해주세요.
- 람다 표현식
  - 함수형 프로그래밍을 위한 람다 표현식이 추가됨
  - 간결하고 가독성이 좋은 코드 작성이 가능해짐

- Stream API
  - 컬렉션을 처리하기 위한 새로운 API 추가
  - 간결한 코드로 병렬 처리 가능

- 인터페이스의 디폴트 메서드
  - 인터페이스에 메서드를 추가할 수 있게 됨
  - 기존에 구현한 클래스에 영향을 주지 않고 인터페이스를 확장할 수 있음

- 메서드 참조
  - 람다 표현식 대신 메서드를 참조할 수 있게 됨
  - 코드 가독성이 향상됨
  - list.forEach(System.out::println); 와 같이 :: 표

- Optional 클래스
  - NullPointerException 방지를 위한 클래스 추가
  - 값이 없는 상황을 처리하기 위한 방법을 제공함

- Date/Time API
  - 새로운 날짜와 시간 API 추가
  - 이전의 Date와 Calendar 클래스보다 편리하고 간결한 사용이 가능해짐

## try-with-resource에 대해서 설명해주세요.
try-with-resources는 Java 7에서 추가된 기능으로, try-catch-finally 구문에서 자원을 해제하는 작업을 보다 간결하게 처리할 수 있게 해줍니다.
기존에는 try-catch-finally 구문에서 자원을 해제하기 위해 finally 블록에서 close() 메서드를 호출하는 코드를 작성해야 했습니다. 그러나 이렇게 작성한 코드는 가독성이 떨어지며, 예외 처리가 필요한 코드에서 불필요한 예외 처리 코드를 추가해야 했습니다. try-with-resources 구문을 사용하면, finally 블록에서 close() 메서드를 호출하는 코드를 작성하지 않아도 됩니다. 대신 try 구문 안에 자원을 선언하면, 자원을 자동으로 해제해줍니다.

EX)
```
try (BufferedReader reader = new BufferedReader(new FileReader("file.txt"))) {
    String line = reader.readLine();
    while (line != null) {
        System.out.println(line);
        line = reader.readLine();
    }
} catch (IOException e) {
    e.printStackTrace();
}
```
추가로, 자바 9 버전에서는 try() 문 안에 명시적으로 객체 선언을 하기 보다는 try 문 바깥에서 객체 선언을 하고 생성된 인스턴스의 변수를 넣어줄 수 있도록 바뀌었습니다.

Java 7 : try(BufferedReader br = new BufferedReader())
Java 9 : try(br)

## 강한 결합과 느슨한 결합이 무엇인지 설명해주세요.
- 강한 결합(Strong coupling) : 하나의 클래스가 다른 클래스에 너무 의존적인 상태를 말합니다. 즉, 한 클래스가 다른 클래스의 내부 구현을 직접 참조하거나, 다른 클래스의 인스턴스를 직접 생성하여 사용하는 것입니다. 이렇게 되면 두 클래스 간의 의존성이 높아지며, 한 클래스의 변경이 다른 클래스에 영향을 주기 쉬워져 유지보수가 어려워집니다.

- 느슨한 결합(Loose coupling) : 클래스 간의 의존성을 최소화하여 클래스들 간의 결합도를 낮추는 것을 말합니다. 클래스 간의 인터페이스나 추상 클래스를 이용하여 구현 세부 내용을 외부에서 숨기고, 인터페이스나 추상 클래스를 통해서만 상호작용하도록 하는 것이 좋습니다. 이렇게 하면 클래스 간의 의존성이 낮아져 유지보수성과 확장성이 좋아집니다.

강한 결합은 개발 초기에는 간편하게 구현할 수 있지만, 시간이 지남에 따라 코드를 변경하거나 유지보수를 할 때 문제가 발생할 수 있습니다. 따라서, 느슨한 결합을 유지하며 클래스 간의 관계를 최대한 단순하게 유지하는 것이 좋습니다.

## 직렬화와 역직렬화에 대해서 설명해주세요.
- 직렬화(Serialization) : 자바 객체를 바이트 형태로 변환하는 것을 말합니다. 객체를 직렬화하면, 해당 객체를 파일이나 네트워크 전송 등에 사용할 수 있습니다. 자바에서는 Serializable 인터페이스를 구현함으로써 객체를 직렬화할 수 있습니다.

- 역직렬화(Deserialization) : 직렬화된 바이트 형태의 객체를 다시 자바 객체로 변환하는 것을 말합니다. 역직렬화를 하면, 직렬화된 객체를 다시 사용할 수 있습니다.

자바 직렬화는 JVM의 메모리에서만 상주되어있는 객체 데이터를 영속화(Persistence)가 필요할 때 사용됩니다. 시스템이 종료되더라도 없어지지 않는 장점을 가지며 영속화된 데이터이기 때문에 네트워크로 전송이 가능합니다.

## 자바의 동시성 이슈(공유자원 접근)에 대해 설명해주세요.
동시에 여러 스레드가 하나의 자원에 접근할 때 발생하는 문제입니다. 동시에 공유자원에 접근해서 값을 수정하는 경우, 예상과는 다른 값으로 수정될 수 있습니다.
자바에서 동시성 문제를 해결하는 방법에는 크게 3가지가 있습니다.

1. Synchronized
synchronized 가 선언된 블럭에는 동시에 하나의 스레드만 접근할 수 있습니다. synchronized 메서드에 접근 시 블록 전체에 lock을 걸게됩니다. 따라서 해당 스레드가 블럭을 빠져나가기 전까지 다른 스레드들은 동기화 처리된 블록에 접근할 수 없습니다. 하지만, 다른 스레드들은 아무런 작업을 하지 못하고 기다릴 수밖에 없어 자원의 낭비가 발생할 수 있습니다. 매우 간단한 해결방법이 될 수 있지만, critical section의 크기및 실행시간에 따라 성능하락 및 자원낭비가 매우 심해지게 됩니다.

2. volatile
JVM에서 스레드는 실행되고 있는 CPU 메모리 영역에 데이터를 캐싱 합니다. (CPU Cache) 따라서 멀티 코어 프로세서에서 다수의 스레드가 변수 a를 공유하더라도 캐싱 된 시점에 따라 데이터가 다를 수 있으며, 서로 다른 코어의 스레드는 데이터 값이 불일치하는 문제가 생길 수 있습니다. 이런 경우 volatile 키워드를 사용하여 CPU 메모리 영역에 캐싱 된 값이 아니라 항상 최신의 값을 가지도록 메인 메모리 영역에서 값을 참조하도록 할 수 있습니다. 즉, 동일 시점에 모든 스레드가 동일한 값을 가지도록 동기화 할 수 있습니다. 하지만 원자성이 보장되지 않는 경우 동시성 문제는 동일하게 발생한다. 

3. Atomic 클래스
1번의 성능저하, 2번의 여전히 남아있는 동시성 문제들을 해결할 수 있는 클래스들입니다. concurrent 패키지의 클래스라고도 하며, 동시성을 다룰 때 매우 유용하게 사용되며, 멀티 스레드 환경에서 안전하게 동작할 수 있도록 설계되어 있습니다.

## Mutable 객체와 Immutable 객체의 차이점에 대해 설명해주세요.
- Mutable 객체 : 객체 생성 이후에도 객체의 상태를 변경할 수 있는 객체를 말합니다. 예를 들어, ArrayList나 HashMap과 같은 자료구조는 요소를 추가하거나 삭제할 수 있으므로 Mutable 객체입니다.

- Immutable 객체 : 객체 생성 이후에는 객체의 상태를 변경할 수 없는 객체를 말합니다. 즉, 객체 생성 후에는 내부 상태가 변경될 수 없으며, 상태를 변경하려면 새로운 객체를 생성해야 합니다. 대표적인 예시로는 String 클래스나 Integer 클래스와 같은 불변 클래스가 있습니다.

Mutable 객체는 여러 스레드에서 동시에 접근하면 객체 상태가 예상치 못하게 변경될 수 있으므로, 스레드 안전성 문제가 발생할 가능성이 높습니다. 반면, Immutable 객체는 내부 상태를 변경할 수 없으므로 스레드 안전성이 보장됩니다.

## 자바에서 null을 안전하게 다루는 방법에 대해 설명해주세요.
- null 검사 : null을 안전하게 다루기 위해서는 null 검사를 수행해야 합니다. null 검사를 수행하여 null이 아닌 경우에만 메서드를 호출하거나 변수를 참조하도록 합니다.

- Optional 클래스 사용 :Java 8부터는 Optional 클래스를 제공하여 null 처리를 안전하게 수행할 수 있습니다. Optional 클래스는 null 값 처리를 안전하게 수행할 수 있는 방법을 제공합니다.

- null 대신 기본값 사용 : 객체의 값이 null인 경우, 대신 기본값을 사용하는 것도 안전한 방법 중 하나입니다. 예를 들어, 문자열이 null인 경우 대신 빈 문자열을 사용하거나, 숫자가 null인 경우 대신 0을 사용하는 것입니다.

- Null Object 패턴 : Null Object 패턴은 null을 대신할 수 있는 객체를 생성하여 사용하는 방법입니다. 이러한 객체는 일반적으로 NullObject 클래스와 같이 null 객체와 같은 인터페이스를 구현합니다. 이 패턴은 null 체크를 감추고, null을 사용해도 안전한 코드를 작성할 수 있도록 도와줍니다.

## Wrapper class란 무엇인가요?
자바의 기본 자료형(primitive data type)인 int, char, boolean 등을 객체로 다루기 위해 제공하는 클래스를 말합니다. 이러한 Wrapper class는 기본 자료형을 객체로 감싸주는 래퍼(wrapper) 역할을 수행합니다.

기본자료형을 객체로 다루어야하는 상황들
- 메서드의 매개변수로 객체를 요구하는 경우 : 기본 자료형을 매개변수로 전달할 수 없는 경우, Wrapper class를 사용하여 객체를 전달해야 합니다.
- 제네릭(Generic)에서 사용하는 경우 : 제네릭은 객체 타입을 파라미터로 받으므로, 기본 자료형을 사용할 수 없습니다. 이 경우, Wrapper class를 사용하여 객체를 전달해야 합니다.
- Collection 객체에 저장하는 경우 : Collection은 객체만을 저장할 수 있기 때문에, 기본 자료형을 직접 저장할 수 없습니다. 이 경우, Wrapper class를 사용하여 객체를 생성한 후 Collection에 저장해야 합니다.
- 객체 직렬화(Serialization)하는 경우 : 객체 직렬화는 객체를 파일이나 네트워크를 통해 전송하기 위한 기술입니다. 이 때, 기본 자료형을 사용하는 객체는 직렬화할 수 없기 때문에, Wrapper class를 사용하여 객체를 생성해야 합니다.
- 자바의 다양한 API에서 사용하는 경우 : 자바의 다양한 API에서는 객체를 요구하는 경우가 많습니다. 이 때, 기본 자료형을 사용하는 객체는 Wrapper class를 사용하여 객체로 감싸주어야 합니다.

# 자료구조

## List와 Set의 차이에 대해서 설명해주세요.
- 중복 원소
  - List는 중복된 원소를 허용합니다. 즉, 같은 객체를 중복해서 저장할 수 있습니다.
  - Set은 중복된 원소를 허용하지 않습니다. 따라서, 같은 객체를 중복해서 저장할 수 없습니다.

- 원소 순서
  - List는 원소를 저장한 순서를 유지합니다. 즉, 원소의 인덱스를 이용하여 순서대로 접근할 수 있습니다.
  - Set은 원소의 저장 순서를 보장하지 않습니다. 따라서, 저장 순서대로 접근할 수 없으며, 순서와 관련된 기능을 사용할 수 없습니다.

- 구현 클래스
  - List 인터페이스를 구현하는 클래스로는 ArrayList, LinkedList, Vector 등이 있습니다.
  - Set 인터페이스를 구현하는 클래스로는 HashSet, TreeSet 등이 있습니다.

## Hash Function, HashTable에 대해서 설명해주세요.
해시 함수(Hash Function)는 임의의 길이의 데이터를 고정된 길이의 데이터로 매핑하는 함수를 말합니다. 해시 함수는 입력값에 따라 항상 고정된 크기의 출력값을 반환하며, 입력값이 조금만 바뀌어도 출력값이 크게 바뀝니다.

해시 함수는 주로 해시 테이블(Hash Table)에서 사용됩니다. 해시 테이블은 키-값 쌍(key-value pair)을 저장하는 자료구조로, 키를 해시 함수를 이용하여 배열의 인덱스로 변환한 뒤, 해당 인덱스에 값을 저장합니다. 해시 테이블은 키를 검색하고 값을 찾는 데 O(1)의 시간 복잡도를 가지므로, 매우 빠른 검색이 가능합니다.

## Stack, Queue에 대해서 설명해주세요.
- Stack
  - Last-In-First-Out(LIFO) 구조를 가지고 있습니다.
  - 데이터를 쌓아 올리는 구조로, 가장 나중에 쌓인 데이터가 가장 먼저 빠져나갑니다.
  - push() 메서드로 데이터를 추가하고, pop() 메서드로 데이터를 제거합니다.
  - 계산기나 브라우저의 뒤로가기 기능과 같이, 나중에 처리해야 하는 데이터를 일시적으로 저장하는 데 사용됩니다.

- Queue
  - First-In-First-Out(FIFO) 구조를 가지고 있습니다.
  - 데이터를 일렬로 늘어놓는 구조로, 가장 먼저 들어온 데이터가 가장 먼저 나갑니다.
  - offer() 메서드로 데이터를 추가하고, poll() 메서드로 데이터를 제거합니다.
  - 자료의 처리 순서가 중요한 경우에 사용됩니다. 예를 들어, 대기열 처리나 이벤트 처리에 사용됩니다.

## 배열과 링크드 리스트의 차이를 설명해주세요.
- 배열
  - 배열은 데이터를 일렬로 저장하는 자료구조입니다.
  - 인덱스를 이용하여 데이터에 접근할 수 있습니다.
  - 배열은 크기를 미리 지정해야 하며, 크기를 동적으로 변경할 수 없습니다.
  - 또한, 배열은 데이터를 추가하거나 삭제하는 경우, 이전에 저장된 데이터를 이동시켜야 하므로 비용이 높을 수 있습니다.
  
- LinkedList
  - LinkedList는 데이터를 노드(node)라는 단위로 나누어 연결한 구조입니다.
  -각 노드는 데이터와 다음 노드를 가리키는 포인터를 포함합니다.
  - LinkedList는 데이터를 추가하거나 삭제할 때, 이전 노드와 다음 노드의 포인터만 변경하면 되므로 배열보다 효율적입니다.
  - LinkedList는 인덱스를 이용한 데이터 접근이 불가능합니다. 따라서, 특정 노드에 직접 접근하기 위해서는 처음부터 노드를 순회해야 합니다.

배열은 인덱스를 이용하여 빠르게 데이터에 접근할 수 있지만, 크기가 고정되어 있고 추가/삭제가 비효율적입니다. 반면, 링크드 리스트는 크기가 동적으로 조정될 수 있고, 데이터 추가/삭제가 빠르지만, 데이터에 접근하기 위해서는 순회해야 하는 비용이 듭니다.

## HashMap vs LinkedHashMap 차이와 장단점은?
- HashMap
  - HashMap은 해시 테이블(Hash Table)을 사용하여 데이터를 저장합니다.
  - 키와 값의 쌍으로 데이터를 저장하며, 키를 기반으로 검색합니다.
  - 데이터의 순서가 보장되지 않습니다.
  - null 값을 허용하며, 동기화를 지원하지 않습니다.
  - 데이터 추가/삭제와 검색에 대해 O(1)의 시간 복잡도를 가지므로, 매우 빠른 속도로 처리가 가능합니다. 하지만, 해시 충돌이 발생하는 경우 성능이 저하될 수 있습니다.

- LinkedHashMap
  - LinkedHashMap은 해시 테이블과 연결 리스트(Linked List)를 조합하여 데이터를 저장합니다.
  - 데이터의 삽입 순서가 유지됩니다. 즉, 데이터가 저장된 순서대로 순회할 수 있습니다.
  - null 값을 허용하며, 동기화를 지원하지 않습니다.
  - HashMap과 달리 데이터의 순서가 유지되기 때문에, 데이터 순서에 대한 정렬이 필요할 때 유용합니다.
  - 데이터 추가/삭제와 검색에 대해 O(1)의 시간 복잡도를 가지므로, HashMap과 마찬가지로 매우 빠른 속도로 처리가 가능합니다. 하지만, 해시 충돌이 발생하는 경우에는 HashMap과 마찬가지로 성능이 저하될 수 있습니다.

HashMap은 데이터 순서가 중요하지 않은 경우에 사용하며, 빠른 검색 속도가 필요한 경우에 적합합니다. 반면, LinkedHashMap은 데이터의 순서가 유지되어야 하거나, 데이터의 순서에 대한 정렬이 필요한 경우에 사용하면 좋습니다.

## 시간복잡도와 공간복잡도는?
- 시간복잡도
  - 알고리즘의 수행 시간을 분석하는 방법입니다.
  - 일반적으로 입력 크기 n에 대한 연산 횟수를 나타냅니다.
  - 대개 O 표기법(Big-O notation)을 사용하여 표기합니다.
  - O(1)은 입력 크기에 관계없이 일정한 시간이 걸리는 알고리즘을 의미하며, O(n), O(n^2) 등은 입력 크기에 따라 연산 횟수가 증가하는 알고리즘을 의미합니다.
  
- 공간복잡도
  - 알고리즘의 메모리 사용량을 분석하는 방법입니다.
  - 일반적으로 입력 크기 n에 대한 메모리 사용량을 나타냅니다.
  - 대개 O 표기법을 사용하여 표기합니다.
  - 공간복잡도는 알고리즘의 수행 시간보다 중요도가 낮지만, 메모리 사용량이 많아지면 알고리즘의 성능에 영향을 미칠 수 있습니다.

보통 시간복잡도와 공간복잡도는 반비례하는 경향이 있습니다.
