# 기본형 매개변수와 참조형 매개변수의 차이
  - 기본형 매개변수를 가지는 메서드는 저장된 값 자체를 받아옴 -> 변수의 값을 변경하여도 다른 변수에는 영향 x
  - 참조형 매개변수를 가지는 메서드는 주소 값을 받아옴 -> 변수의 값을 변경하면 다른 변수에도 영향 o
    
코드
```java
class Data {
	int x = 10;
}

public class Main {
	public static void main(String[] args) {
		Data d = new Data();
		
		System.out.println("Data 객체의 x변수 초기 값 : " + d.x);
		System.out.println(); // 공백
		
		primative(d.x); // 기본형 매개변수를 사용한 메서드
		System.out.println("Data 객체의 x변수 값 : " + d.x); // 값 변경 안됨
		
		System.out.println(); // 공백
		
		reference(d); // 참조형 매개변수를 사용한 메서드
		System.out.println("Data 객체의 x변수 값 : " + d.x); // 값 변경 됨
	}
	
	// 기본형 매개변수
	public static void primative(int x) {
		System.out.println("기본형 매개변수를 가지는 메서드 실행");
		x = 100; // x변수(기본형 변수)의 값 변경
	}
	
	// 참조형 매개변수
	public static void reference(Data d) {
		System.out.println("참조형 매개변수를 가지는 메서드 실행");
		d.x = 100; // d객체(참조형 변수)의 x변수 값 변경
	}
}
```
결과
```java
Data 객체의 x변수 초기 값 : 10

기본형 매개변수를 가지는 메서드 실행
Data 객체의 x변수 값 : 10 (값 변경 x)

참조형 매개변수를 가지는 메서드 실행
Data 객체의 x변수 값 : 100 (값 변경 o)

```
