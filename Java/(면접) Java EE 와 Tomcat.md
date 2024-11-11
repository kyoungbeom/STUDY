# JAVA EE (Enterprise Edition)
    JAVA EE는 JAVA SE를 기반으로 하는 표준 스펙

    JAVA EE는 엔터프라이즈 애플리케이션을 구축하기 위한 다양한 API와 컴포넌트(예: EJB, JSP, Servlets, JPA 등)를 제공 

    JAVA EE는 인터페이스와 규약을 정의하며, 직접 실행할 수 없음. 대신, 이러한 스펙을 구현한 웹 애플리케이션 서버(WAS)가 필요함

# JAVA EE 구현체

###  TOMCAT
    TOMCAT은 JAVA EE 스펙의 일부를 구현한 경량화된 WAS임 
    특히, 서블릿(Servlet)과 JSP(JavaServer Pages) 사양을 구현하여 웹 애플리케이션을 지원함 

    TOMCAT은 전체 JAVA EE 스펙을 구현하지 않기 때문에 '경량화'된 WAS(정확히는 Web Container)로 분류됨
    전체 JAVA EE 스펙을 구현한 WAS는 JBoss, WebLogic, WebSphere 등이 있음.
    (엄연히 따지면, TOMCAT은 WAS보다는 웹 컨테이너에 가까움. 완벽한 WAS가 되기 위해서는 JAVA EE 스펙 전체를 구현해야 함)

### TOMCAT의 구성
    TOMCAT의 웹 컨테이너는 서블릿 컨테이너와 JSP 컨테이너를 포함하고 있음 
    이 컨테이너는 서블릿과 JSP 파일을 자바 클래스 파일로 변환하고, 이 클래스 파일을 객체로 생성하여 실행함 

    WAS에서 생성된 서블릿 객체들은 서블릿 컨테이너에서 관리되며, 이는 JAVA SE의 객체로 처리됨 
    즉, 서블릿 컨테이너는 JAVA EE 스펙을 따라 객체를 생성하고 관리하지만, 이 객체들은 JAVA SE 환경에서 실행됨
