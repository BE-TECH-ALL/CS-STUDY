# Java
## JVM의 구조와 Java의 실행방식을 설명해주세요.
- 자바 가상 머신(Java Virtual Machine)인 JVM의 역할은 자바 애플리케이션을 클래스 로더를 통해 읽어 자바 API와 함께 실행하는 것이다.

### JVM의 구조
- 클래스 로더(Class Loader) 
  - 로드된 바이트 코드(.class)들을 엮어서 JVM의 메모리 영역인 Runtime Data Areas에 배치한다.
  
- 실행 엔진(Execution Engine)
  - 클래스 로더를 통해 런타임 데이터 영역에 배치된 바이트 코드를 명령어 단위로 읽어서 실행한다
  
- 런타임 데이터 영역 (Runtime Data Area)
  - JVM의 메모리 영역으로 자바 애플리케이션을 실행할 때 사용되는 데이터들을 적재하는 영역이다.
  
- JNI - 네이티브 메소드 인터페이스 (Native Medthod Interface)
  - 자바가 다른 언어로 만들어진 어플리케이션과 상호 작용할 수 있는 인터페이스 제공하는 프로그램이다.
  
- 네이티브 메소드 라이브러리 (Native Method Library)
  - C, C++로 작성된 라이브러리를 칭한다.

### Java의 실행방식
- 자바 컴파일러(javac)가 자바 소스코드(.java)를 읽어 자바 바이트코드(.class)로 변환시킨다.
- Class Loader를 통해 class 파일들을 JVM으로 로딩한다.
- 로딩된 class파일들은 Execution engine을 통해 해석된다.
- 해석된 바이트 코드는 Runtime Data Areas에 배치되어 실직적인 수행이 이루어진다.


## GC가 무엇인지, 필요한 이유는 무엇인지, 동작방식에 대해 설명해주세요.
- 가비지 컬렉션(Garbage Collection, 이하 GC)은 자바의 메모리 관리 방법 중의 하나로 JVM(자바 가상 머신)의 Heap 영역에서 동적으로 할당했던 메모리 중 필요 없게 된 메모리 객체(garbage)를 모아 주기적으로 제거하는 프로세스를 말한다.
- 이 객체를 제거하는 작업이 필요한 이유는 자바는 개발자가 메모리를 직접 해제해줄 수 없는 언어이기 때문이다.
- 가비지 컬렉션이 될 대상 객체를 식별(Mark)하고 제거(Sweep)하며 객체가 제거되어 파편화된 메모리 영역을 앞에서부터 채워나가는 작업(Compaction)을 수행하게 된다.

## 컬렉션 프레임워크에 대해서 설명해주세요.
- Java Collection은 널리 알려져 있는 자료구조를 바탕으로 객체, 데이터들을 효율적으로 관리 할 수 있는 자료구조들이 있는 라이브러리를 컬렉션 프레임워크라고 합니다.
- List, Set은 Collection 인터페이스을 상속받지만, Map 인터페이스는 구조상의 차이라 별도로 정의합니다.

## 제네릭에 대해서 설명해주세요.
- 제네릭은 자바의 타입 안정성을 맡고 있습니다. 컴파일 과정에서 타입체크를 해주는 기능으로 객체의 타입을 컴파일 시에 체크하기 때문에 객체의 타입 안정성을 높이고 형변환의 번거로움을 줄여줍니다.

## 애노테이션에 대해서 설명해주세요.
- 어노테이션은 작성한 코드에 대해 추가적인 정보를 제공하면서 컴파일 타임 혹은 런타임 시점에서 해당 코드에 필요한 추가적인 처리를 해 주는 역할을 한다.

## 오버라이딩과 오버로딩이 무엇이며 어떤 차이가 있을까요?

오버로딩(overloading)
같은 이름의 메소드를 중복하여 정의하는 것을 의미한다.
즉, 서로 다른 시그니처를 갖는 여러 메소드를 같은 이름으로 정의하는 것이다.
오버로딩은 OOP특징인 다형성을 구현하는 방법 중 하나다.

오버라이딩(overriding)
부모클래스의 메서드를 자식클래스에서 같은 시그니쳐를 갖는 메소드로 재정의하는 것이다.
부모클래스의 메소드보다 접근 제어자를 더 좁은 범위로 변경할 수 없다.
부모클래스의 메소드보다 더 큰 범위의 에외를 선언할 수 없다.

> 메소드 시그니쳐(Method signature)
메소드의 선언부에 명시되는 매개변수의 리스트를 말한다.
만약 두 메소드가 매개변수의 개수와 타입, 그 순서까지 모두 같다면, 두 메소드의 시그니처는 같다고 할 수 있다.


## 인터페이스와 추상클래스의 차이점에 대해 설명해주세요.
추상클래스는 객체의 추상적인 상위 개념으로 공통된 개념을 표현할 때 사용합니다. 단일 상속만 가능합니다. 추상클래스를 상속하는 집합간에는 연관관계가 있습니다.

인터페이스는 구현 객체가 같은 동작을 한다는 것을 보장하기 위해 사용합니다. 다중 상속이 가능합니다. 인터페이스를 구현하는 집합간에는 관계가 없을 수 있습니다.

## 클래스는 무엇이고 객체는 무엇인가요?
클래스는 객체를 정의하는 틀 또는 설계도와 같은 의미로 사용됩니다.

객체는 식별 가능한 개체 또는 사물입니다. 객체는 구별 가능한 식별자, 특징적인 행동, 변경 가능한 상태를 가집니다. 인스턴스들을 통칭하는 용도로 사용합니다.

## 정적(static)이란 무엇인가요?
static은 클래스 멤버라고 하며, 클래스 로더가 클래스를 로딩해서 메소드 메모리 영역에 적재할 때 클래스별로 관리됩니다.

static 키워드를 통해 생성된 정적멤버들은 PermGen 또는 Metaspace에 저장되며 저장된 메모리는 모든 객체가 공유하며 하나의 멤버를 어디서든지 참조할 수 있는 장점이 있습니다.

그러나, GC의 관리 영역 밖에 존재하기 때문에 프로그램 종료시까지 메모리가 할당된 채로 존재합니다. 너무 남발하게 되면 시스템 성능에 악영향을 줄 수 있습니다.

## 자바의 원시타입들은 무엇이 있으며 각각 몇 바이트를 차지하나요?
boolean(1), char(unsigned 2), byte(1), short(2), int(4), long(8), float(4), double(8)

사실 JVM에 의존적이기 때문에 정확한 크기라기 보다는 대략적인 크기입니다.

## 접근 제어자의 종류와 이에 대해 설명해주세요.
private, default, protected, public이 있습니다. private은 해당 클래스 내에서만 접근 가능하고, default는 해당 패키지, protected는 상속한 클래스, public은 전체 영역에서 접근 가능합니다.

접근 제어자를 사용하는 이유는 외부에 보여주고 싶은 정보들을 선택적으로 제공하기 위함이고, 캡슐화와 통하는 면이 있습니다.

## 객체지향에 대해서 설명해주세요.
프로그램 구현에 필요한 객체를 파악하고 각각의 객체들의 역할이 무엇인지를 정의하여 객체들 간의 상호작용을 통해 프로그램을 만드는 것을 말한다.

## SOLID(객체지향 5대원칙)에 대해서 설명해주세요.
SRP(단일책임원칙)은 한 클래스의 하나의 책임만 가져야 합니다.

OCP(개방-폐쇄 원칙)은 확장에는 열려 있으나 변경에는 닫혀 있어야 하며, 다형성을 활용해야 합니다.

LSP(리스코프 치환 원칙)은 프로그램의 객체는 프로그램의 정확성을 깨뜨리지 않으면서 하위 타입의 인스턴스로 바꿀 수 있어야하는 원칙으로 상위 타입을 상속해서 재정의 했을 때 프로그램이 깨지지 않아야 합니다.

ISP(인터페이스 분리 원칙)은 클라이언트는 자신이 사용하지 않는 메서드에 의존 관계를 맺으면 안되는 원칙입니다. 특정 클라이언트를 위한 인터페이스 여러 개가 범용 인터페이스 하나보다 더 낫습니다. 즉, 비대한 인터페이스보단 더 작고 구체적인 인터페이스로 분리해야합니다.

DIP(의존관계 역전 원칙)은 추상적인 것은 자신보다 구체적인 것에 의존하지 않고, 변화하기 쉬운 것에 의존해서는 안된다는 원칙입니다. 구체적으론 구현 클래스에 의존하지 말고, 인터페이스에 의존해야 하는 원칙입니다.

## 동일성(identity)와 동등성(equality)에 대해 설명해주세요. (equals(), ==)
동일성은 객체의 주소를 비교하는 것이고, 동등성은 객체의 같음을 비교하는 것입니다.

기본적으로 자바에서는 Object 클래스에 정의된 equals() 메소드가 동일성 비교를 합니다. 따라서, 개발자는 원한다면 equals() 메소드를 오버라이딩해서 동등성의 판단 기준을 정의해주면 됩니다.

## 원시타입과 참조타입의 차이에 대해 설명해주세요.
원시타입은 항상 값이 존재해야 합니다. 반면, Object 타입은 null 포인터를 가질 수 있습니다. 그리고 멤버변수가 초기화될 때, 원시타입은 기본값을 가지지만, 참조타입은 null 포인터를 가지는 차이도 있습니다.

## String, StringBuilder, StringBuffer 각각의 차이에 대해 설명해주세요.
String은 불변입니다. StringBuilder와 StringBuffer는 이런 String의 특징때문에 사용하는 가변타입이라고 볼 수 있습니다.

StringBuilder와 StringBuffer는 Thread-safe 여부의 차이가 있습니다. StringBuilder는 Thread-safe하지 않습니다. 따라서 Multi-Thread 환경에서 사용할 때는 StringBuffer를 사용합니다.

## Checked Exception과 Unchecked Exception에 대해 설명해주세요. 
체크 예외(Checked Exception)
체크 예외는 RuntimeException의 하위 클래스가 아니면서 Exception 클래스의 하위 클래스들입니다. 체크 예외의 특징은 반드시 에러 처리를 해야하는 특징(try/catch or throw)을 가지고 있습니다.

언체크 예외(Unchecked Exception)
언체크 예외는 RuntimeException의 하위 클래스들을 의미합니다. 이것은 체크 예외와는 달리 에러 처리를 강제하지 않습니다.
말 그대로 실행 중에(runtime) 발생할 수 있는 예외를 의미합니다.


## Java 11을 사용하는 이유
좀 더 알아봐야 함...

## 강한 결합과 느슨한 결합이 무엇인지 설명해주세요.
느슨한 결합(Loose Coupling)은 다른 클래스를 직접적으로 사용하는 클래스의 의존성을 줄이는 것이고 강한 결합(Tight Coupling)은 클래스와 객체가 서로 의존하고 있는 것이다

## 직렬화와 역직렬화에 대해서 설명해주세요.
직렬화란 자바 시스템 내부에서 사용되는 객체 또는 데이터를 외부의 자바 시스템에서도 사용할 수 있도록 바이트 형태로 데이터 변환하는 기술과 바이트로 변환된 데이터를 다시 변환하는 기술(역직렬화)을 아울러서 이야기 합니다.

## 자바의 동시성 이슈(공유자원 접근)에 대해 설명해주세요.
동일한 하나의 데이터에 2 이상의 스레드, 혹은 세션에서 가변 데이터를 동시에 제어할 때 나타는 문제입니다.


## Mutable 객체와 Immutable 객체의 차이점에 대해 설명해주세요.
Mutable한 객체는 생성된 이후에 상태가 변경될 수 있는 객체이고, Immutable한 객체는 생성된 이후에 상태가 변경되지 않는 객체를 말한다.

## 자바에서 null을 안전하게 다루는 방법에 대해 설명해주세요.
공개 메서드가 아닌 곳에는 assert를 사용하여 null을 방어할 수 있습니다. 또한 메서드의 인자를 받을 때 Objects.requireNonNull()을 사용하여 방어할 수 있습니다. 그리고 Optional을 사용해 리턴 타입에서 null을 반환하지 않도록 방어할 수 있습니다. 마지막으로 사전 조건과 사후 조건을 명확히 하여 계약에 의한 설계를 실천해야 합니다.


# 자료구조/알고리즘
## 배열과 링크드 리스트의 차이를 설명해주세요.
배열은 메모리상에 순서대로 데이터를 저장합니다. 반면 링크드 리스트는 다음 데이터의 위치에 대한 포인터를 가지고 있는 구조입니다.

배열은 데이터를 인덱스로 조회할 수 있기 때문에 인덱스 조회성능이 높고, 데이터가 메모리에 순서대로 저장되어 있기 때문에, 캐시의 지역성으로 인하여 비교적 빠르게 탐색을 수행할 수 있습니다.

링크드 리스트는 중간에 데이터를 삽입하거나 삭제하는 것이 용이하다는 장점이 있습니다.

## List와 Set의 차이에 대해서 설명해주세요.
List는 중복된 데이터를 저장하고 순서를 유지하는 선형 자료구조이고, Set은 중복되지 않은 데이터를 저장할 수 있고, 일반적으로 순서를 유지하지 않는 선형 자료구조입니다.

## Hash Function, HashTable에 대해서 설명해주세요.
Hash Function
- 데이터의 효율적 관리를 목적으로 임의의 길이의 데이터를 고정된 길이의 데이터로 매핑하는 함수

HashTable
- 해시 테이블은 (Key, Value)로 데이터를 저장하는 자료구조 중 하나로 빠르게 데이터를 검색할 수 있는 자료구조이다



## Stack, Queue에 대해서 설명해주세요.
Stack
스택은 선형 자료구조의 일종으로 마지막에 저장한 데이터를 가장 먼저 꺼내게 되는 LIFO(Last In First Out)방식의 자료구조 입니다. 스택의 사용 예시로는 웹 브라우저의 방문기록(뒤로가기), 실행 취소(undo) 등이 있습니다.

Queue
큐는 선형 자료구조의 일종으로 처음에 저장한 데이터를 가장 먼저 꺼내게 되는 FIFO(First In First Out)방식의 자료구조 입니다. 큐의 사용 예시로는 프린터의 인쇄 대기, 콜센터 고객 대기 시간 등이 있습니다.

## Heap, Priority Queue에 대해서 설명해주세요.
우선순위 큐(Priority Queue)는 들어간 순서에 상관없이, 우선순위가 높은 데이터가 먼저 나가는 형태의 자료구조이다.
우선순위 큐는 배열, 연결 리스트, 힙으로 구현이 가능하다.
이 중에서 힙(Heap)을 이용하여 구현하는 것이 가장 효율적이다.

힙은 Complete Binary Tree(완전 이진 트리) 이다.
모든 노드에 저장된 값(우선순위)들은 자식 노드들의 것보다 (우선순위가) 크거나 같다.


## Tree, Binary Tree, BST, AVL Tree에 대해서 설명해주세요.
Tree : 트리는 계층적 관계를 표현하는 자료구조이다.
Binary Tree : 이진트리는 각 노드가 최대 두 개의 자식 노드를 갖는 트리이다.
BST(Binary Search Tree) : 이진 탐색 트리란 정렬된 이진트리
AVL Tree : AVL 트리는 스스로 균형을 잡는 이진 탐색 트리

## BST의 최악의 경우의 예와 시간복잡도에 대해서 설명해주세요.
평균적인 경우 O(log(N))의 시간복잡도를 가진다.
최악의 경우 O(N)의 시간복잡도를 가진다.
![image](https://user-images.githubusercontent.com/111635735/230717315-68cb11d8-75d3-439f-a0b0-447d5c93254e.png)
출처 : https://navigator-ymin.tistory.com/2


## DFS, BFS에 대해서 설명해주세요.
BFS, DFS 두가지 모두 그래프를 탐색하는 방법
DFS 깊이를 우선으로 탐색하고, BFS는 너비를 우선으로 탐색합니다.


## 정렬, 탐색에 대해 설명해주세요.
정렬이라는 것은 리스트를 순서대로 정리만 하는 것이고, 탐색은 특정 값을 리스트에서 찾는 것입니다.
