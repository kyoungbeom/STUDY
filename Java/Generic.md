# 제네릭
    Biz.service 메서드에 인자로 list2를 주면 컴파일 에러가 발생
```java
import java.util.*;

public class Test {

	public static void main(String[] args) {
		List<A> list=new ArrayList<A>();
		//list.add("java");
		//list.add(new String("java"));
		//list.add(new StringBuilder("java"));
		//list.add(1);
		list.add(new A());
		list.add(new B());
		
		List<B> list2=new ArrayList<B>();
		list2.add(new B());
		Biz.service(list2); 
		
	}

}

class A{
	
}
class B extends A{
	
}
class Biz{
	public static void service(List<A> list) {
		for(A a:list) {
			System.out.println(a);
		}
	}
}
```
    ? extends A 와 같은 형태로 와일드 카드를 사용하면 컴파일 에러가 없어짐
```java
import java.util.*;

public class Test {

	public static void main(String[] args) {
		List<A> list=new ArrayList<A>();
		//list.add("java");
		//list.add(new String("java"));
		//list.add(new StringBuilder("java"));
		//list.add(1);
		list.add(new A());
		list.add(new B());
		
		List<B> list2=new ArrayList<B>();
		list2.add(new B());
		Biz.service(list2); 
		
	}

}

class A{
	
}
class B extends A{
	
}
class Biz{
	public static void service(List<? extends A> list) {
		for(A a:list) {
			System.out.println(a);
		}
	}
}
```
