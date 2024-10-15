# JVM(Java Virtual Machine)
    자바 가상머신의 약자로서, OS와 자바 어플리케이션 사이를 중재해주는 기술이다
    
    JVM은 클래스로더를 통해 클래스를 로드하고 링킹하며, Execution Engine을 통해 실제로 실행한다. 
    Garbage Collector는 힙 메모리에서 불필요한 객체를 삭제하여 메모리를 관리하고, Runtime Data Area는 실행에 필요한 여러 메모리 영역을 제공한다.

![image](https://github.com/KYOUNGBEOM/STUDY/assets/112946948/97d767c0-3600-4529-bcc2-80cc2abc652c)

# 추가 설명

### Execution Engine
    1. 인터프리터
    바이트코드를 한 줄씩 해석하여 즉시 실행한다

    2. JIT 컴파일러
    자주 실행되는 바이트코드를 기계어로 변환하여 성능을 최적화한다
    JIT 컴파일러는 자주 호출되는 메서드를 식별하고, 이를 한 번만 식별하여 빠르게 실행할 수 있도록 한다   

    3. 더 알아보기
    자주 사용되는 메서드에 대해서만 JIT 컴파일러가 사용되고 그 이외에 코드에 대해서는 인터프리터가 사용

### 자바의 작동 과정
    1. JVM이 OS로부터 적당한 메모리(Runtime Data Area)를 할당 받습니다.

    2. 자바 소스 코드(.java)를 자바 컴파일러(javac)를 통해 바이트 코드(.class)로 변환합니다

    3. 클래스로더를 통해 .class 파일을 메모리(Runtime Data Area)에 로딩합니다.

    4. 로딩된 클래스 파일(바이트 코드)을 Execution Engine을 통해 기계어로 변환하고 실행합니다.
