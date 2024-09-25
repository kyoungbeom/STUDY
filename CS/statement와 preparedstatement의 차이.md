# Statement와 PreparedStatement 차이점
    둘 다 Java에서 데이터베이스와 상호작용하기 위한 객체로, SQL 쿼리를 실행할 때 사용. 

    하지만 이 둘은 사용 방식과 성능, 보안 측면에서 차이가 있음.

## 1. Statement
    SQL 쿼리를 실행하기 위한 기본 객체

    - SQL 쿼리의 동적 실행: 
      동적으로 SQL 쿼리를 실행. 즉, 쿼리를 실행할 때마다 SQL 문을 데이터베이스에 전달하고 실행.
      
    - SQL 쿼리의 매번 파싱: 
      쿼리를 실행할 때마다 매번 데이터베이스에서 파싱 및 컴파일 과정을 거침.
      
    - 보안 문제:
      SQL 쿼리에 직접 변수를 삽입하는 방식이기 때문에 SQL Injection 공격에 취약. 
      예를 들어, 사용자가 입력한 값을 쿼리문에 직접 포함시키기 때문에 악의적인 SQL을 주입할 가능성이 多.

### 사용 예시
```java
Statement stmt = connection.createStatement();
String query = "SELECT * FROM users WHERE username = '" + username + "'";
ResultSet rs = stmt.executeQuery(query);
```
## 2. PreparedStatement
    미리 컴파일된 SQL 쿼리를 실행하기 위한 객체로, 성능 및 보안 측면에서 더 나은 옵션.

### 특징:

    - 미리 컴파일된 SQL 
      SQL 쿼리를 미리 컴파일하여 재사용. SQL 문이 데이터베이스에 전달될 때, 처음 한 번만 파싱 및 컴파일이 이루어지며, 
      이후에는 이미 준비된 쿼리를 재사용하기 때문에 성능이 더 좋음.
  
    - SQL Injection 방지
      쿼리와 값이 별도로 처리되기 때문에 SQL Injection 공격에 안전. 
      사용자가 입력한 값은 따로 전달되므로, 악의적인 SQL 코드를 주입하더라도 이를 값으로 처리하여 보안을 강화.
  
    - 파라미터 바인딩
      쿼리 내에서 `?`를 사용하여 파라미터를 바인딩 가능. 이를 통해 값만 변경하면서 같은 쿼리를 여러 번 실행 가능.

### 사용 예시:
```java
String query = "SELECT * FROM users WHERE username = ?";
PreparedStatement pstmt = connection.prepareStatement(query);
pstmt.setString(1, username); // 첫 번째 ?에 username 값을 바인딩
ResultSet rs = pstmt.executeQuery();
```

## SQL Injection 예시

### 상황 설정
    사용자가 로그인하기 위한 웹 애플리케이션이 있으며, 사용자 이름과 비밀번호를 입력받는 폼이 있음. 
    이 정보는 다음과 같이 SQL 쿼리로 처리.

### 취약한 코드 예시
    아래의 Statement 객체를 사용한 코드에서는 사용자가 입력한 정보를 그대로 SQL 쿼리에 포함.

```java
// 사용자 입력을 그대로 사용
String username = request.getParameter("username");
String password = request.getParameter("password");

// 취약한 SQL 쿼리
String query = "SELECT * FROM users WHERE username = '" + username + "' AND password = '" + password + "'";

Statement stmt = connection.createStatement();
ResultSet rs = stmt.executeQuery(query);
```

    사용자가 다음과 같은 값을 입력한다고 가정

    - username : `admin' --`
    - password : (공백)

위의 입력을 쿼리에 적용하면 다음과 같은 쿼리가 생성

```sql
SELECT * FROM users WHERE username = 'admin' --' AND password = ''
```
여기서 --는 SQL에서 주석 처리 기호. 즉, 쿼리는 다음과 같이 해석

```sql
SELECT * FROM users WHERE username = 'admin'
```

    결과적으로, 이 쿼리는 admin이라는 사용자 이름을 가진 계정을 찾는 쿼리로 변형되며, 비밀번호 조건은 무시됨. 
    만약 데이터베이스에 admin 계정이 존재한다면, 공격자는 인증 없이 해당 계정으로 접근가능

