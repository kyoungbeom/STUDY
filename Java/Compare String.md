# String 타입의 비교
    Java에서 String은 참조형 변수이며, 따라서 메모리에는 객체의 주소가 저장됨
    참초형 변수를 비교할 때 '==' 연산자를 사용하면 두 String 객체의 실제 주소를 비교

    그러나 equals() 메서드는 String 클래스에서 이미 오버라이드되어 있어서 
    객체의 내용(즉, 문자열의 값)을 비교하도록 설계되어 있음
    
    따라서 equals() 메서드를 사용하면 두 String 객체의 내용이 동일한지 비교가능

# String 타입 비교 예시
```java
String s1 = "Hello";
String s2 = "Hello";

System.out.println(s1 == s2);          // true (같은 문자열 리터럴을 참조하므로 같은 객체)
System.out.println(s1.equals(s2));     // true (값이 동일하므로 true)
```

```java
String s1 = new String("Hello");
String s2 = new String("Hello");

System.out.println(s1 == s2);          // false (새로운 객체가 생성되므로 주소가 다름)
System.out.println(s1.equals(s2));     // true (값이 동일하므로 true)
```
    
