# 두 수의 비교 결과에 따른 작동 방식
    음수일 경우 : 두 원소의 위치를 교환 안함
    
    양수일 경우 : 두 원소의 위치를 교환 함

# Comparable 
    자기 자신과 매개변수 객체를 비교 
```java
public class ClassName implements Comparable<Type> { 
 
/*
  ...
  code
  ...
 */
 
	// 필수 구현 부분
	@Override
	public int compareTo(Type o) {
		/*
		 비교 구현
		 */
	}
}
```
# Comparator
    두 매개변수 객체를 비교
```java
import java.util.Comparator;	// import 필요
public class ClassName implements Comparator<Student> { 
 
/*
  ...
  code
  ...
 */
 
	// 필수 구현 부분
	@Override
	public int compare(Student o1, Student o2) {
		/*
		 비교 구현
		 */
	}
}
```
