# Singleton
```java
public class Test {
	
	public static void main(String[] args) {
		A obj1 = A.getInstance();
		obj1.i++;
		System.out.println(obj1.i);
		
		A obj2 = A.getInstance();
		obj2.i++;
		System.out.println(obj2.i);
		
		System.out.println(obj1 == obj2);
		
		
	}
}

class A {
	
	int i = 10;
	
	private A () {}
	
	// 싱글톤 패턴
	private static A instance = null;
	
	public static A getInstance() {
		if(instance == null) {
			instance = new A();
		} 
		
		return instance;
	}
}
```
