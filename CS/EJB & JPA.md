# EJB(Enterprise JavaBean)
  - Java EE의 구성요소로, 기업용 어플리케이션 서버 측 컴포넌트를 개발하기 위한 기술
  - 분산 객체 컴퓨팅을 지원하여, 대규모 기업 환경에서 복잡한 비즈니스 로직을 쉽게 구현가능

# EJB 구성 요소
  1. 세션 빈(Session Bean)
      - 클라이언트와 상호작용 담당
      - Stateless Session Bean 과 Stateful Session Bean으로 나뉨
       
  2. 엔티티 빈(Entity Bean) -> 현재는 JPA(Java Persistence API)로 대체됨
      - 데이터베이스와의 상호작용 담당
      - 데이터를 영속화시킴 
        
  3. 메시지 구동 빈(Message-Driven Bean)
      - 비동기 메세지를 처리
    
  # EJB 컨테이너
    - EJB는 EJB 컨테이너라는 실행환경에서 동작
    - 자동으로 빈의 생명주기를 관리
    - 트랜잭션을 자동으로 관리하여 데이터 일관성 유지

  # JPA(Java Persistence API)란?
    - 자바 객체와 관계형 데이터베이스 간의 매핑을 관리하는 표준 API
    - 자바 어플리케이션에서 데이터베이스 작업을 쉽게 할 수 있도록 도와주는 도구

  # JPA 구성 요소
    1. 엔티티(Entity)
        - 자바 객체와 데이터베이스 간의 매핑을 처리해주는 클래스

    2. 엔티티 매니저(Entity Manager)   
        - 엔티티 객체를 생성, 읽기, 업데이트, 삭제하는데 사용되는 인터페이스
        - 트랜잭션 관리, 쿼리 처리, 커넥션 관리, 영속성 컨텍스트 관리

    3. 영속성 컨텍스트(Persistence Context)
        - 엔티티 매니저가 엔티티 객체를 관리하는 환경
        - 엔티티의 상태를 추적하고, 트랜잭션 동안 변경된 내용을 데이터베이스에 반영
