# 멀티스레드란?
    자바에서의 멀티스레드는 동시에 여러 작업을 처리하는 방식을 지원하는 개념이다.

    java.lang.Thread 클래스를 통해 스레드를 직접 생성하거나, Runnable 인터페이스를 구현하여 멀티스레딩을 지원한다.

# Thread 생성방법
    1. Thread 클래스를 상속받는 방법
    Thread 클래스를 상속받아 run() 메서드를 오버라이딩한다.

    2. Runnable 인터페이스를 구현하는 방법
    Runnable 인터페이스의 run() 메서드를 구현한 후, 이를 Thread 클래스 생성자의 인자로 전달하여 스레드를 생성한다.

```
// Runnable 인터페이스 구현 예시
class MyRunnable implements Runnable {
    public void run() {
        System.out.println("Thread is running.");
    }
}

// 스레드 실행
Thread thread = new Thread(new MyRunnable());
thread.start();
```

# Thread 관리 방법
    스레드를 직접 관리하는 대신 자바는 Executor 프레임워크를 제공하여 더 효율적으로 스레드를 관리할 수 있다.
    이 프레임워크는 스레드 풀을 제공하여, 스레드의 생성/종료/재사용이 가능하다.
    
    ExecutorService 인터페이스를 사용하면 된다.
