[참고] https://hoons-dev.tistory.com/72

# 스프링이란?
    자바 기반의 엔터프라이즈 어플리케이션 개발을 위한 오픈 소스 프레임워크이다.
    스프링은 IoC(Inversion of Control)와 DI(Dependency Injection)라는 핵심 개념을 중심으로 설계되어 있다.
    이를 통해 객체 간의 의존성을 쉽게 관리하고 코드 결합도를 낮출 수 있다.

# IoC란?
    제어의 역전을 의미하는 IoC는 객체의 생성과 의존성 관리를 외부 컨테이너(예: 스프링 컨테이너)에게 맡기는 설계 패턴이다.
    일반적으로 객체는 자신이 사용할 의존성을 직접 생성하거나 관리하지만, IoC에서는 컨테이너가 객체의 생명 주기를 관리하고 필요한 의존성을 객체에 주입해 준다.
    IoC 덕분에 객체는 필요한 의존성을 외부에서 받아오므로, 객체 생성과 의존성 주입을 분리할 수 있어 결합도가 낮아진다.

### 예시
    만약 A라는 클래스가 B라는 클래스에 의존한다고 가정할 때, 일반적으로 A 클래스는 B의 인스턴스를 직접 생성하여 사용한다. 
    하지만 IoC에서는 스프링 컨테이너가 B의 인스턴스를 생성하고, A가 필요할 때 컨테이너가 B를 A에게 주입한다. 
    따라서 A 클래스는 B의 생성 방식에 대해 알 필요가 없고, 외부에서 주입되는 B를 사용하게 된다.

# DI란?
    의존성 주입(Dependency Injection)은 IoC를 구현하는 방법 중 하나이다. 
    DI에서는 객체가 자신이 사용할 의존성을 직접 생성하지 않고, 외부에서 전달받는다.

    DI는 의존성 주입 방법에 따라 생성자 주입, 세터(setter) 주입, 필드 주입 등으로 나뉜다.

    생성자 주입: 의존성이 생성자를 통해 객체에 전달된다.
    세터 주입: 세터 메서드를 통해 객체가 생성된 후 의존성을 주입한다.
    필드 주입: 필드에 직접 주입하여 사용한다. (보통은 권장되지 않으며, 테스트에 주로 사용됨)

# 결론
    IoC는 객체의 생성과 관리를 스프링 컨테이너가 담당하는 것이고, DI는 이렇게 생성된 객체들 간의 의존성을 외부에서 주입하여 연결하는 과정이다.

# 스프링 컨테이너
    스프링의 두 가지 주요 컨테이너는 BeanFactory와 ApplicationContext이다. 
    이 중 ApplicationContext는 BeanFactory의 기능을 포함한 더 기능이 풍부한 컨테이너로, 일반적으로 스프링 애플리케이션에서 주로 사용된다.

# 객체 등록 방법
    스프링 컨테이너에 객체를 등록하는 방법에는 크게 XML 설정과 어노테이션 기반 설정이 있다.

### XML
```
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
           http://www.springframework.org/schema/beans/spring-beans.xsd">

    <bean id="myBean" class="com.example.MyClass"/>
</beans>
```

### 어노테이션
    스프링 2.5 버전부터는 어노테이션 기반 설정이 지원되며, 
    @Component, @Service, @Repository, @Controller 등 다양한 애노테이션을 사용해 클래스를 자동으로 스프링 컨테이너에 등록할 수 있다. 
    
    이를 위해 @Configuration 또는 @ComponentScan과 같은 애노테이션을 사용해 설정 파일에 스캔 범위를 지정하고, 
    그 범위 내에서 @Component가 붙은 클래스들을 자동으로 등록한다.
```
@Component
public class MyClass {
    // ...
}

@Configuration
@ComponentScan(basePackages = "com.example")
public class AppConfig {
    // MyClass는 자동으로 스프링 컨테이너에 등록됨
}
```
