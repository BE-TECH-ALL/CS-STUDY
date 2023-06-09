# Java의 특징과 장단점에 대해 설명해주세요.
자바는 자바 가상 머신(JVM, Java Virtual Machine)을 사용하여 운영체제와 독립적으로 동작할 수 있다. 

따라서 자바는 어느 운영체제에서나 같은 형태로 실행 될 수 있다.
* 장점
  - 객체 지향 언어로 클래스 계층 구조, 상속성, 다형성 ,캡슐화 지원
  - 하드웨어, 운영체제 종류와 관계없이 독립적 실행이 가능
* 단점
  - 프로그램 개발 시 발생할 수 있는 예외를 직접 처리해야하며, 그렇지 않으면 컴파일 시에 오류가 발생
  - JVM에 의해 기계어로 번역되고 실행되는 과정을 거치기 때문에, 컴파일 되자마자 기계어로 변환되는 C, C++에 비해 속도가 느림

# JVM의 역할에 대해 설명해주세요.
JVM이란 Java Virtual Machine 의 줄임말로, Java Byte Code 를 운영체제에 맞게 해석해주는 역할을 합니다. 즉, 작성한 자바 프로그램의 실행 환경을 제공하는 자바 프로그램의 구동 엔진입니다.
Java compiler 는 .java 파일을 .class 라는 자바 바이트코드로 변환시켜주는데 Byte Code 는 기계어(Native Code)가 아니므로 OS 에서 바로 실행이 되지 않습니다. 이때 JVM은 OS가 Byte Code 를 이해할 수 있도록 해석해주는 역할을 담당합니다.
JVM은 메모리 관리도 담당합니다. 이를 '가비지 컬렉터'라고 하는데, 가비지 컬렉터는 Java7부터 힙 영역의 객체들을 관리하는 역할을 담당합니다.

# Java의 컴파일 과정에 대해 설명해주세요.
1. 개발자가 자바 소스코드(.java)를 작성합니다.

2. 자바 컴파일러(Java Compiler)가 자바 소스파일을 컴파일합니다. 이때 나오는 파일은 자바 바이트 코드(.class)파일로 아직 컴퓨터가 읽을 수 없는 자바 가상 머신이 이해할 수 있는 코드입니다. 바이트 코드의 각 명령어는 1바이트 크기의 Opcode와 추가 피연산자로 이루어져 있습니다.

3. 컴파일된 바이크 코드를 JVM의 클래스로더(Class Loader)에게 전달합니다.

4. 클래스 로더는 동적로딩(Dynamic Loading)을 통해 필요한 클래스들을 로딩 및 링크하여 런타임 데이터 영역(Runtime Data area), 즉 JVM의 메모리에 올립니다.

5. 실행엔진(Execution Engine)은 JVM 메모리에 올라온 바이트 코드들을 명령어 단위로 하나씩 가져와서 실행합니다. 이때, 실행 엔진은 두가지 방식으로 변경합니다.
- 인터프리터 : 바이트 코드 명령어를 하나씩 읽어서 해석하고 실행합니다. 하나하나의 실행은 빠르나, 전체적인 실행 속도가 느리다는 단점을 가집니다.
- JIT 컴파일러(Just-In-Time Compiler) : 인터프리터의 단점을 보완하기 위해 도입된 방식으로 바이트 코드 전체를 컴파일하여 바이너리 코드로 변경하고 이후에는 해당 메서드를 더이상 인터프리팅 하지 않고, 바이너리 코드로 직접 실행하는 방식입니다. 하나씩 인터프리팅하여 실행하는 것이 아니라 바이트 코드 전체가 컴파일된 바이너리 코드를 실행하는 것이기 때문에 전체적인 실행속도는 인터프리팅 방식보다 빠릅니다.

#  Java에서 제공하는 원시 타입들에 무엇이 있고, 각각 몇 바이트를 차지하나요?
![image](https://github.com/BE-TECH-ALL/CS-STUDY/assets/67897318/364f5c86-766a-476d-80fe-c0e35473d09b)

# 싱글톤 패턴에 대해 설명해주세요.
싱글톤(Singleton) 패턴의 정의는 단순하다. 객체의 인스턴스가 오직 1개만 생성되는 패턴을 의미합니다.

# 생성자(Constructor)에 대해 설명해주세요.
인스턴스가 생성될 때 호출되는 인스턴스 초기화 메서드이다. *인스턴스 변수의 초기화 작업에 주로 사용되며, 인스턴스 생성 시에 실행되어야 할 작업을 위해 사용된다.

# Wrapper Class란 무엇이며, Boxing과 UnBoxing은 무엇인지 설명해주세요.
래퍼(Wrapper) 클래스는 기본 자료형(int, double, boolean 등)의 데이터를 인스턴스(객체)로 만들기 위해 사용(포장) 하는 클래스이다. 
박싱(boxing)은 기본 자료형의 데이터를 래퍼(wrapper) 클래스의 객체로 만드는 과정을 의미하며,
언박싱(un boxing)은 래퍼(wrapper) 클래스의 데이터를 기본 자료형으로 얻어내는 과정을 말한다.
(예 : int → Integer 박싱(boxing) / Integer → int 언박싱(un boxing))

# 접근 제한자(Access Modifier)에 대해 설명해주세요.
접근 제한자(Access Modifier)는 말 그대로 접근을 제한하기 위해 사용됩니다. 여기서 접근이란 클래스 및 인터페이스 그리고 이들이 가지고 있는 멤버의 접근을 말합니다. 
접근 제한자는 public, protected, private와 같이 세 가지 종류가 있습니다.

- public 접근 제한자: 단어 뜻 그대로 외부 클래스가 자유롭게 사용할 수 있도록 합니다.
- protected 접근 제한자: 같은 패키지 또는 자식 클래스에서 사용할 수 있도록 합니다.
- private 접근 제한자: 단어 뜻 그대로 개인적인 것이라 외부에서 사용될 수 없도록 합니다.

#  Error와 Exception의 차이를 설명해주세요.
에러는 메모리 부족이나 스택오버플로우와 같이 발생하면 복구할 수 없는 심각한 오류이고, 예외는 발생하더라도 수습할 수 있는 비교적 덜 심각한 오류입니다. 이 예외는 프로그래머가 적절히 코드를 작성해주면 비정상적인 종류를 막을 수 있습니다.

# Stack과 Queue 구조에 대해 설명해주세요.
스택(Stack) 자료구조는, 책을 쌓는 것처럼 차곡차곡 쌓아 올린 형태의 자료구조를 의미한다.
즉, 후입선출(LIFO, Last In First Out) 방식의 자료구조이다.

큐(Queue) 는 "줄을 서서 기다린다."라는 사전적 의미를 가지고 있다.
따라서, 큐 (Queue) 자료구조는, 먼저 들어온게 먼저 나가는 선입선출(FIFO, First In FirstOut) 방식의 자료구조이다.

# Tree와 Heap의 구조에 대해 설명해주세요.
Tree는 Node와 Branch를 이용해서, 사이클을 이루지 않도록 구성한 데이터 구조입니다. 
Heap은 트리를 기반으로 변형된 형태의로 완전 이진 트리의 일종으로 우선순위 큐를 위하여 만들어진 자료구조입니다.

데이터에서 최대값과 최소값을 빠르게 찾기 위해 고안된 완전 이진 트리(Complete Binary Tree)이며, 우선순위 큐와 같이 최대값, 최소값을 빠르게 찾아야 하는 자료구조, 알고리즘에 활용될 수 있음
힙 트리에서는 중복된 값을 허용한다.

# Priority Queue(우선순위 큐)에 대해 설명해주세요.
일반적인 큐(Queue)는 먼저 집어넣은 데이터가 먼저 나오는 FIFO (First In First Out) 구조로 저장하는 선형 자료구조입니다.

하지만 우선순위 큐(Priority Queue)는 들어간 순서에 상관없이 우선순위가 높은 데이터가 먼저 나오는 것을 말합니다.

우선순위 큐는 다음과 같은 속성을 가지고 있습니다.

모든 항목에는 우선순위가 있습니다.
우선 순위가 높은 요소는 우선 순위가 낮은 요소보다 먼저 queue에서 제외됩니다.
두 요소의 우선 순위가 같으면 queue의 순서에 따라 제공됩니다.

# Array와 ArrayList의 차이점에 대해 설명해주세요.
Array는 고정 길이의 배열로서 초기화시 배열의 크기를 지정한다. 배열을 초기화시 메모리가 할당되어 
속도가 빠르다는 장점이 있다. 또한 데이터의 순서가 있고 또 데이터의 중복을 허용한다.

ArrayList는 List 컬렉션 인터페이스의 한 종류로서 배열의 크기를 실행 타임에 정하는 가변 길이를 갖는 배열이다.
그렇기 때문에 메모리가 재할당되어 Array의 비해 속도가 느리다는 단점이 있다.
또한 Array와 마찬가지로 데이터의 순서가 있으며 데이터의 중복을 허용한다.

# 시간복잡도와 공간복잡도는?
- 시간복잡도

알고리즘의 수행 시간을 분석하는 방법입니다.
일반적으로 입력 크기 n에 대한 연산 횟수를 나타냅니다.
대개 O 표기법(Big-O notation)을 사용하여 표기합니다.
O(1)은 입력 크기에 관계없이 일정한 시간이 걸리는 알고리즘을 의미하며, O(n), O(n^2) 등은 입력 크기에 따라 연산 횟수가 증가하는 알고리즘을 의미합니다.

- 공간복잡도

알고리즘의 메모리 사용량을 분석하는 방법입니다.
일반적으로 입력 크기 n에 대한 메모리 사용량을 나타냅니다.
대개 O 표기법을 사용하여 표기합니다.
공간복잡도는 알고리즘의 수행 시간보다 중요도가 낮지만, 메모리 사용량이 많아지면 알고리즘의 성능에 영향을 미칠 수 있습니다.
 
