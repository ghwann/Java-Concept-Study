### 1주차 과제 : JVM은 무엇이며 자바 코드는 어떻게 실행하는 것인가

---



#### 목표

---

자바 소스 파일(.java)을 JVM으로 실행하는 과정 이해하기



#### 학습할 것

<hr>

* JVM이란 무엇인가
* 컴파일 하는 방법
* 실행하는 방법
* 바이트코드란 무엇인가
* JIT 컴파일러란 무엇이며 어떻게 동작하는지
* JVM 구성 요소
* JDK와 JRE의 차이



### 1. JVM이란?

<hr>

- Java Virtual Machine(자바 가상 머신)의 약자, 자바 바이트코드를 실행할 수 있는 주체
- 모든 자바 가상 머신은 자바 가상 머신 규격에 정의된 대로 자바 바이트코드를 실행하는데 자바 바이트코드는 플랫폼에 독립적 
  - 따라서 표준 자바 API까지 동일한 동작을 하도록 구현한 상태에서는 이론적으로 모든 자바 프로그램은 CPU나 운영 체제의 종류와 무관하게 동일하게 동작

![#자바가상머신, JVM(Java Virtual Machine)이란 무엇인가?](https://img1.daumcdn.net/thumb/R800x0/?scode=mtistory2&fname=https%3A%2F%2Ft1.daumcdn.net%2Fcfile%2Ftistory%2F25616D45576B854C3F)

출처 : [https://asfirstalways.tistory.com/158](https://asfirstalways.tistory.com/158)



### 2. JVM의 구성요소

---

 - Class Loader(클래스 로더)

   	- JVM내로 클래스(.class)를 로드하고 링크를 통해 배치하는 작업을 수행하는 모듈
   	- Runtime 시 동적으로 클래스를 로드
   	- jar파일 내 저장된 클래스들을 JVM 위에 탑재하고 사용하지 않는 클래스들은 메모리에서 삭제
   	- 자바는 동적코드, 컴파일 타임이 아니라 런타임에 참조
   	- 즉, 클래스를 처음으로 참조할 때 해당 클래스를 로드하고 링크하는 것

- Execution Engine(실행 엔진)

  - 클래스를 실행시키는 역할

  - 클래스 로더가 JVM 내의 런타임 데이터 영역에 바이트코드를 배치시키고 이것은 실행 엔진에 의해 실행

  - 자바 바이트코드는 자바 가상 머신이 이해할 수 있는 언어로 변환된 자바 소스 코드이며 자바 컴파일러로 변환되는 코드의 명령어 크기가 1바이트라서 바이트코드임

  - 이때 위와 같은 바이트코드를 실행 엔진이 두 가지 방법으로 실제로 JVM 내부에서 기계가 실행할 수 있는 형태로 변경

    - Interpreter(인터프리터)

       실행 엔진은 자바 바이트코드를 명령어 단위로 읽어서 실행 → 이 방식은 한 줄 씩 수행하기 때문에 느린 인터프리터 언어의 단점을 가지고 있음

    - JIT(Just-In-Time)

      ① 인터프리터 방식의 단점을 보완하기 위해 도입된 JIT 컴파일러

      ② 런타임 시 클래스파일(바이트코드)를 네이티브 기계어로 한방에 컴파일 후 사용하는 개념

    - Garbage Collector

      GC를 수행하는 모듈(쓰레드)이 있음



#### JVM의 특성

---

- 스택 기반의 가상 머신
- 단일 상속 형태의 객체 지향 프로그래밍을 가상 머신 수준에서 구현
- 포인터를 지원하되 C와 같이 주소 값을 임의로 조작이 가능한 포인터 연산이 불가능
- 가비지 컬렉션 사용
- 모든 기본 타입의 정의를 명확히 함으로써 플랫폼 독립성 보장
- 데이터 흐름 분석에 기반한 자바 바이트코드 검증기를 통해 스택 넘침, 명령어 피연산자의 타입 규칙 위반, 필드 접근 규칙 위반, 지역 변수의 초기화 전 사용 등 많은 문제를 실행 전에 검증하여 실행 시 안전을 보장하고 별도의 부담을 줄여줌