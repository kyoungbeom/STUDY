# 실행과정
  1. JVM이 OS로부터 적당한 메모리(Runtime Data Area)를 할당 받습니다.

  2. 자바 소스 코드(.java)를 자바 컴파일러(javac)를 통해 바이트 코드(.class)로 변환합니다

  3. 클래스로더를 통해 .class 파일을 메모리(Runtime Data Area)에 로딩합니다.

  4. 로딩된 클래스 파일(바이트 코드)을 Execution Engine을 통해 기계어로 변환하고 실행합니다.
