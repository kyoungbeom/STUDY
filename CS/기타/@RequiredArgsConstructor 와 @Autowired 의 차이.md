# 공통점
- 기본적으로 Type을 기준으로 의존성을 주입(DI)함
- 동일한 Type의 빈(Bean)이 여러개 존재할 경우 참조 변수의 이름과 동일한 빈(Bean)을 찾아서 의존성을 주입함
- @Qualifier 어노테이션을 사용하거나 @Bean의 name 속성을 사용하여 의존성 주입 간의 충돌을 예방할 수 있음
  
![image](https://github.com/user-attachments/assets/f935e195-bf41-4e83-a24a-e6735c113e03)

# Autowired 정의 및 특징
- 필드주입, 메서드주입, 생성자 주입이 가능함
- 만약 메서드 주입이나 필드주입할 경우 set메서드를 사용해서 주입하기 때문에, 객체가 NULL일 가능성이 존재함
- 필드주입과 메서드 주입의 차이점은 필드 주입은 객체가 생성되는 시점에 주입되지만, <br>
  메서드 주입은 특정 메서드가 호출되는 시점에 주입됨

# 필드주입 또는 메서드 주입 방식으로 사용할 때의 단점
1. NullPointerException 발생 가능성
    - 테스트 코드의 중요성이 부각되고 있는 만큼, <br>
      의존성 주입이 제대로 이루어지지 않을 가능성이 존재하는 Autowired는 사용을 지양하는것이 좋음 <br>
      (단, 필드주입, 메서드주입 방식에 한함, 생성자 주입은 안전함)

2. final 옵션을 사용할 수 없기 때문에 코드가 변질될 가능성이 존재함

3. 순환 참조 에러 발생 가능
    - 아래 그림과 같이 UserService가 이미 MemberService에 의존하고 있는 상황에서, <br>
      MemberService도 UserService에 의존하면 순환 참조 에러가 발생함 <br>
      (springboot 2.6 버전 이후에서는 순환 참조가 기본적으로 허용되지 않음)

![image](https://github.com/user-attachments/assets/d510c338-24fc-44a9-8a87-9a3b74c01629)

![image](https://github.com/user-attachments/assets/e1a646ed-bbe4-496a-9095-34e8bd36fd14)

<br>

# RequiredArgsConstructor 정의 및 특징
- 생성자 주입 방식 어노테이션으로, 생성자로 의존성을 주입하는 방법
- final 키워드가 붙은 필드에 대해 생성자로 의존성을 주입함
- Lombok dependecy를 추가해야만 사용할 수 있음
- 스프링 개발팀에서 권장하는 방식임

# RequiredArgsConstructor 장점
1. 객체의 불변성 확보
    - 기본적으로 final 키워드가 붙은 필드에 대해 생성자로 주입을 하기 때문에, 객체의 불변성이 확보됨 <br>
      또한, 의존성이 주입이 생성자를 통해 이루어지기 때문에,
      객체가 생성되는 시점에 의존성 주입이 이루어지고 이를통해 NullPointerException을 예방할 수 있음

![image](https://github.com/user-attachments/assets/1252d9ea-4ac3-4ecb-abac-a462878be081)

2. 테스트 코드 작성 용이
    - 생성자를 통해 의존성을 주입하므로, 테스트 시 필요한 목(Mock) 객체를 생성자를 통해 쉽게 주입할 수 있음 <br>

3. 순환 참조 에러 방지
    - 순환 참조가 발생하면 생성자가 호출되지 않기 때문에, 이러한 상황을 컴파일 타임에서 미리 잡아낼 수 있음
