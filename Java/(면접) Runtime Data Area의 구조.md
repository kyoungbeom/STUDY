# Runtime Data Area의 구조
    런타임 데이터 영역은 6가지 영역으로 나누어짐
    이 6가지 영역은 다시 JVM 단위와 스레드 단위로 나누어짐
    
    1. 메서드 영역
    2. 힙 영역
    3. 런타임 상수풀
    4. pc register
    5. JVM 스택
    6. Native 메서드 스택

![image](https://github.com/user-attachments/assets/e0e08f19-cb6f-4674-bdb0-d2fba9fca0bf)

# JVM 단위
    JVM이 시작될 때 단 하나만 생성되며, 모든 스레드들이 공유한다

    1. 메서드 영역
       클래스와 인터페이스, 메서드, 필드, static 멤버, final 멤버 등이 저장되는 영역

    2. 힙 영역
       JVM 실행 중 객체를 생성하는 영역으로, new 키워드를 사용하여 생성한 모든 객체와 배열이 저장됨
       가비지 컬렉터에 의해 자동으로 관리됨
    
![image](https://github.com/user-attachments/assets/31b7bbda-d3f5-4766-9190-9e8faa9b33a2)

# 스레드 단위
    1. pc register
       JVM이 바이트 코드를 실행할 때, 어떤 바이트 코드를 실행할지를 나타내는 주소를 저장하는 영역
  
    2. JVM 스택
       메서드 호출과 관련된 정보를 저장하는 영역으로, 지역변수, 메서드 매개변수, 반환 주소 등이 저장됨
       LIFO 구조로 작동함
  
    3. Native 메서드 스택
       자바가 아닌 다른 언어로 작성된 네이티브 메서드의 호출 정보를 저장하는 영역
     
![image](https://github.com/user-attachments/assets/c31eb777-9fc1-4982-bdf7-ac054ba7f564)
