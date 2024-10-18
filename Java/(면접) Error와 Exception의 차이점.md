# Error
    자바에서 심각한 시스템 레벨의 문제이다.

    java.lang.error 패키지에 속한다

    런타임 시점에 발생하여, 컴파일 시점에는 알 수 없다

    에러는 복구 불가능하다

    모든 에러는 Unchecked Type로 명시적 예외처리가 선택적이다.

    예시로는 OutOfMemory나 StackOverFlow가 있다.

# Exception
    java.lang.exception 패키지에 속한다

    checked Type, Unchecked Type으로 분류할 수 있다.

    checked Exception은 컴파일 시점에, Unchecked Exception은 런타임 시점에 알 수 있다.

    checked Type 예외는 반드시 try-catch 구문으로 반드시 예외 처리 해주어야 한다.
