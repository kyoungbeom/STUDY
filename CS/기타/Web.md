  # 웹서버(Web Server)
  - HTTP를 통해 웹브라우저에서 요청하는 HTML파일이나 오브젝트(이미지 파일 등)을 전송해주는 서비스 프로그램
   
  - 웹 초창기에는 복잡한 동적 처리를 하지 않았기 때문에 웹서버만으로 처리가능
    
  - 초기에는 웹 서버와 어플리케이션 서버를 명확히 구분하지 않고 웹 서버라는 용어로 통칭했지만, <br>
    서버 부하 관리와 성능 최적화를 위해 웹 서버와 어플리케이션 서버로 나누게 됨

# CGI (Common Gateway Interface)
  - CGI는 웹서버와 외부프로그램 사이에서 정보를 주고 받는 방법, 표준 스펙이자 인터페이스를 의미
    
  - 동적인 데이터를 처리하기 위해 등장한 기술
  
  - 어플리케이션이 동적인 데이터를 반환하려면 요청에 맞는 프로그램(A)뿐만 아니라, <br>
    알맞는 프로그램(A)를 적절히 넘겨주는 중간 역할을 하는 프로그램(B)가 필요한데, 이때 CGI가 프로그램(B)의 역할을 함

  - 기존 기술을 가지고 웹에 억지로 적용시켰기 때문에, 요청당 프로세스 단위로 처리를 하고, 플랫폼에 종속적인 문제 등이 발생 <br>
    이러한 문제를 해결한 썬의 기술 이름이 Servlet, Servlet의 개발 불편성을 해소한 기술이름이 JSP

  - CGI는 주로 웹서버 위에서 작동

# 어플리케이션 서버(Application Server)
  - 웹 서비스가 복잡해지고 기능이 다양해지며(데이터 변경, 사용자 구별 처리, 비즈니스 로직 수행), <br>
    웹 서버 하나에서 모든 로직을 처리하기에는 부하가 커서 별도의 서버가 필요하게 되었고, 이가 어플리케이션 서버
    
  - 어플리케이션 서버는 복잡한 동적 처리(비즈니스 로직, 트랜잭션)를 주로 하며, 데이터베이스 서버와 함께 작동
    
  - 어플리케이션 서버가 동적이라고 불리는 이유는, <br>
    HTTP 프로토콜을 통해 브라우저에게 요청된 데이터를 전송하기 전 어플리케이션 서버가 실시간으로 데이터를 처리하고 업데이트하기 때문
    
# 웹 어플리케이션 서버(Web Application Server)
  - J2EE(Java 2 Enterprise Edition)의 스펙을 구현하여, servlet이나 JSP로 작성된 어플리케이션을 실행하는 소프트웨어
    
  - WAS는 어플리케이션 서버의 한 종류임
    
  - WAS는 서블릿 컨테이너를 포함하고 있음

# 웹 컨테이너
![image](https://github.com/user-attachments/assets/efce9243-1010-476e-bd36-0fa38e693aa6)

# 서블릿 컨테이너
  - 서블릿을 만들었다고 해서 스스로 작동하지 않음 <br>
    서블릿을 생성, 소멸, 관리해주는 것이 필요한데, 이 역할을 하는 것이 서블릿 컨테이너
    
  - 서블릿 컨테이너는 IoC(Inversion of Control) 및 DI(Dependency Injection)을 지원하여 서블릿의 생명주기와 의존성 관리를 자동으로 처리

# WAS와 서블릿 컨테이너의 차이점
    WAS는 웹 서버처럼 HTTP 요청과 응답을 할 수 있고, 
    응답시 필요한 데이터베이스나 외부 서비스와의 교류 비즈니스 로직을 처리할 수 있음 
    
    이때, WAS는 비즈니스 로직이나 트랜잭션을 처리할 때 서블릿을 사용하는데, 
    이러한 서블릿 관리를 서블릿 컨테이너가 함 
    
    즉, 대부분의 WAS는 서블릿 컨테이너를 포함하고 있음 <br>

![image](https://github.com/user-attachments/assets/18e50c3f-93c7-442d-a2b5-397b3631ebe1)

# JAVA SE와 JAVA EE 

## 1. JAVA SE (Standard Edition)

JAVA SE는 크게 JRE(실행)와 JDK(실행, 개발)로 나누어짐

### JRE

JRE (Java Runtime Environment): 자바 애플리케이션을 실행하기 위한 환경 <br>
JRE는 JVM과 기본 자바 클래스 라이브러리(rt.jar)를 포함하고 있으며, 애플리케이션 실행만 가능

### JDK

JDK (Java Development Kit): 자바 애플리케이션을 개발하기 위한 도구 모음 <br>
JDK는 JRE를 포함하고 있으며, 추가적으로 컴파일러(javac), 디버거, 문서 생성기 등을 제공 <br>
JDK는 자바 애플리케이션을 개발하고 실행하는 데 필요한 모든 도구를 제공

### JVM의 역할

JVM은 자바 애플리케이션을 실행하는 핵심 역할을 하며, JAVA SE와 JAVA EE에서 공통적으로 사용됨 <br>
JVM은 바이트코드 검증기(byteCode Verifier)와 JIT Compiler(Just-in-time compiler)를 가지고, <br>
이를 기반으로 바이트코드를 해석하고, 실제 머신 코드로 변환하여 애플리케이션을 실행함 <br>

![image](https://github.com/user-attachments/assets/7ab00f96-4b55-475f-9f7a-31df930f4280)

## 2. JAVA EE (Enterprise Edition)

JAVA EE는 JAVA SE를 기반으로 하는 표준 스펙 <br>
JAVA EE는 엔터프라이즈 애플리케이션을 구축하기 위한 다양한 API와 컴포넌트(예: EJB, JSP, Servlets, JPA 등)를 제공 <br>
JAVA EE는 인터페이스와 규약을 정의하며, 직접 실행할 수 없음. 대신, 이러한 스펙을 구현한 애플리케이션 서버(WAS)가 필요함

# JAVA EE 구현체

###  TOMCAT
TOMCAT은 JAVA EE 스펙의 일부를 구현한 경량화된 WAS임 <br>
특히, 서블릿(Servlet)과 JSP(JavaServer Pages) 사양을 구현하여 웹 애플리케이션을 지원함 <br>

TOMCAT은 전체 JAVA EE 스펙을 구현하지 않기 때문에 '경량화'된 WAS(정확히는 Web Container)로 분류됨 <br>
전체 JAVA EE 스펙을 구현한 WAS는 JBoss, WebLogic, WebSphere 등이 있음.
(엄연히 따지면, TOMCAT은 WAS가 아님. 완벽한 WAS가 되기 위해서는 JAVA EE 스펙 전체를 구현해야 함) <br>

### TOMCAT의 구성

TOMCAT의 웹 컨테이너는 서블릿 컨테이너와 JSP 컨테이너를 포함하고 있음 <br>
이 컨테이너는 서블릿과 JSP 파일을 자바 클래스 파일로 변환하고, 이 클래스 파일을 객체로 생성하여 실행함 <br>

서블릿 컨테이너는 서블릿을 관리하고, HTTP 요청과 응답을 처리함 <br>
JSP 컨테이너는 JSP 파일을 서블릿으로 변환하여 처리함.

# 추가설명

### JAVA SE와 객체 관리

WAS에서 생성된 서블릿 객체들은 서블릿 컨테이너에서 관리되며, 이는 JAVA SE의 객체로 처리됨 <br>
즉, 서블릿 컨테이너는 JAVA EE 스펙을 따른 객체를 생성하고 관리하지만, 이 객체들은 JAVA SE 환경에서 실행됨
