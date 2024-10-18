#  new String("")와 ""의 차이
    new 연산자를 사용하여 String 객체를 만들면 Heap영역에 동적 객체가 할당된다.
    예를 들어, 동일한 new String("hello")를 두 번 실행하면, 서로 다른 hello 라는 값을 가진 객체가 두 개 만들어지는 것이다.

    반면 리터럴 방식으로 저장하면 Heap영역안에 Constant pool(상수풀)에 값이 저장된다.
    이 상수풀은 동일한 문자열 리터럴이 사용되었을때 새로운 객체를 만들지않고 상수풀에 있는 객체를 사용하게 만든다.
    예를 들어, String a = "Hello"를 두 번 실행하면, 상수풀에는 hello 객체 하나를 만들어 놓고 재사용한다.

    String a = new String("hello");
    String b = new String("hello");

    a==b -> false

    String c = "hello"
    String d = "hello"

    c==d -> true

![image](https://github.com/user-attachments/assets/5157887e-186a-4fcf-b891-31e17819d0c5)
![image](https://github.com/user-attachments/assets/686eef2f-36fe-4036-acb7-aa2b856c1f86)
