# 다형성이란?
  - 여러가지 형태를 가질 수 있는 능력
  - 조상 클래스 타입의 참조변수로 자손 클래스 인스턴스를 참조할 수 있도록 함
  - 반대로, 자손 클래스 타입의 참조변수로 조상 클래스 인스턴스를 참조하는 것은 불가능함 <br>
  
    그 이유는 참조변수가 사용할 수 있는 멤버의 개수는 참조하고 있는 인스턴스 가지고 있는 멤버의 수와 같거나 적어야 하는데, <br>
    자손 클래스 타입 참조변수로 조상 클래스 인스턴스를 참조하게 되면, 참조변수가 사용할 수 있는 멤버의 개수가 더 많아 지는 경우가 생김 <br>

  - 참조변수의 타입에 따라 사용할 수 있는 인스턴스 멤버 개수가 달라짐

# 참조변수의 형변환
  - 자손타입 -> 조상타입 (묵시적 형변환 가능, Up-casting)
   
  - 조상타입 -> 자손타입 (명시적 형변환, Down-casting)
    
  - 참조변수의 형변환 과정에서는 참조변수가 참조하고 있는 인스턴스가 어떤 것이 확인하는 것이 중요

```java
// 조상 클래스 Car
class Car {
	
}

// car 클래스를 상속한 자손 클래스 Sonata
class Sonata extends Car {
	
}

public class Polymorphism {
	public static void main(String[] args) {
		// 조상클래스 타입의 참조변수가 조상클래스 인스턴스를 참조
		Car car = new Car();
		// 형변환 불가능, 자손클래스 타입의 참조변수로 조상클래스 인스턴스를 참조할 수 없음
		Sonata sonata = (Sonata)car; 
		
		// 조상클래스 타입의 참조변수가 자손클래스 인스턴스를 참조
		car = new Sonata();
		// 형변환 가능, 자손클래스 타입의 참조변수로 자손클래스 인스턴스를 참조할 수 있음
		sonata = (Sonata)car; 
	}
}
```

# instanceof 연산자
  - 참조변수 instanceof 타입(클래스 또는 인터페이스)의 형태로 사용
    
  - insatnceof의 결과가 true라면 형변환이 가능하다는 것이고, false라면 불가능하다는 것 <br>
    또한, true라는 것은 참조변수가 클래스의 자손이거나 인터페이스를 구현하고 있다는 것
    

# 참조변수와 인스턴스의 연결
  - 조상클래스와 자손클래스 사이에 동일한 변수명을 가지는 인스턴스 변수가 존재할 경우 참조변수의 클래스 타입을 기준으로 출력
    
  - 인스턴스 메서드의 경우에는 오버라이딩 된 자손 메서드가 출력
```java
// 조상 클래스 Parent
class Parent {
	int x = 100;
	public String method() {
		return "parent method";
	}
}

// Parent 클래스를 상속한 자손 클래스 Child
class Child extends Parent {
	int x = 200;
	public String method() {
		return "child method";
	}
}

public class Polymorphism {
	public static void main(String[] args) {
		Parent parent = new Child();
		Child child = new Child();
		
		System.out.println("parent.x : " + parent.x); // 200이 출력되어야 할 것 같지만, 100 출력
		System.out.println("parent.method : " + parent.method()); // 오버라이딩 된 자손 메서드 출력
		
		System.out.println(); // 공백
		
		System.out.println("child.x : " + child.x);
		System.out.println("child.method : " + child.method());
	}
}
```
