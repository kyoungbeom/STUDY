# Session
    정의 : 웹 어플리케이션에서 클라이언트와 서버간의 상태를 유지하기 위해 사용하는 방법

    필요성 
           HTTP는 상태를 유지하지 않는 stateless 프로토콜이기 때문에,
           클라이언트쪽에서 여러번 요청을 보내도 서버쪽에서는 해당 클라이언트가 동일한 클라이언트인지 알 수 없음

           따라서 서버쪽에 사용자마다 고유한 sessionId를 생성하여 저장해놓고, 
           생성한 sessionId를 쿠키의 형태로 클라이언트에게 보내 반복되는 요청에 대해 서버가 동일한 클라이언트인지를 판단할 수 있게 해줌.

    장점 
           1. 세션을 통해 사용자의 로그인 상태, 장바구니 정보 등 중요한 상태를 유지할 수 있음
           2. 쿠키에 비해 상대적으로 보안이 뛰어나고, 중요 정보를 서버에 저장하기 때문에 클라이언트측 정보 유출위험이 낮음
           3. 세션 정보가 서버에 저장되므로, 서버측에서 정보 관리와 접근 제어가 용이함

    단점
           1. 세션은 서버 메모리나 데이터베이스에 저장되기 때문에, 많은 사용자가 접속할 경우 서버에 부하가 생길 수 있음
           2. 세션은 설정한 시간동안만 유효하며, 이 시간이 지나면 다시 로그인해야하는 불편함이 있음
           3. 여러대의 서버가 운영되는 환경에서는 세션 관리를 위해 별도의 세션 클러스터링이나 공유 메커니즘이 필요함
<hr>           

# Session 구현 코드
[session.zip](https://github.com/user-attachments/files/16678798/session.zip) (Intellij / Spring Boot / Gradle / zip 파일 다운 받으면 전체코드 다운가능)
```java
package com.example.session.service;

import com.example.session.db.UserRepository;
import com.example.session.model.LoginRequest;
import jakarta.servlet.http.HttpServletRequest;
import jakarta.servlet.http.HttpSession;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;

@Service
public class UserService {

    @Autowired
    private UserRepository userRepository;

    // sessionId를 만드는 방법 1
    public void login1(
            LoginRequest loginRequest,
            HttpSession httpSession
    ) {
        var id = loginRequest.getId();
        var pw = loginRequest.getPassword();

        // 입력받은 id로 DB에 해당 id이 있는지 확인
        var optionalUser = userRepository.findByName(id);

        // db에 입력받은 id가 있다면
        if(optionalUser.isPresent()) {
            // db에 저장되어있던 유저정보를 가져옴
            var userDto = optionalUser.get();

            // db에 저장된 유저정보가 입력받은 비밀번호와 같다면
            if(userDto.getPassword().equals(pw)) {

                // 메서드 호출 시 세션이 없으면 새로운 세션이 생성되고, 이때 sessionId가 만들어짐
                // 만들어진 sessionId는 HTTP 응답의 쿠키에 담겨 클라이언트한테 전달됨
                httpSession.setAttribute("USER", userDto);
            } else {
                throw new RuntimeException("Password Not Match");
            }
        }  else { // 없는 유저
            throw new RuntimeException("User Not Found");
        }
    }

    // sessionId를 만드는 방법 2
    public void login2(
            LoginRequest loginRequest,
            HttpServletRequest request
    ) {
        // 기존의 세션이 존재한다면 세션을 받아오고, 존재하지 않는다면 새로운 세션을 생성
        // getSession() 메서드가 호출되는 순간 서블릿컨테이너가 자동으로 sessionId 생성
        HttpSession session = request.getSession(true); // 여기에 false를 넣으면 세션이 존재하지 않아도 새로운 세션을 만들지 않음
        
        var id = loginRequest.getId();
        var pw = loginRequest.getPassword();

        // 입력받은 id로 DB에 해당 id이 있는지 확인
        var optionalUser = userRepository.findByName(id);

        // db에 입력받은 id가 있다면
        if(optionalUser.isPresent()) {
            // db에 저장되어있던 유저정보를 가져옴
            var userDto = optionalUser.get();

            // db에 저장된 유저정보가 입력받은 비밀번호와 같다면
            if(userDto.getPassword().equals(pw)) {
                // getSession() 메서드에서 이미 sessionId가 생성되었기 때문에, 별도로 생성하지 않음
                session.setAttribute("USER", userDto);
            } else {
                throw new RuntimeException("Password Not Match");
            }
        }  else { // 없는 유저
            throw new RuntimeException("User Not Found");
        }
    }
}
```
<hr>

# Cookie
    정의 : 웹 브라우저와 서버 간의 상태 정보를 저장하고 교환하기 위해 사용하는 작은 데이터 파일

    필요성 :
            HTTP는 상태를 유지하지 않는 stateless 프로토콜이기 때문에, 서버는 클라이언트의 상태를 지속적으로 추적하기 어려움.
            이때 쿠키를 통해 클라이언트의 상태를 서버가 식별하고 유지할 수 있도록 돕기 위해 사용할 수 있음.
            서버는 클라이언트에게 쿠키를 전송하고, 클라이언트는 이후의 요청에 이 쿠키를 포함시켜 서버와의 상태를 유지할 수 있음.

    장점
           1. 쿠키를 통해 사용자의 로그인 상태, 개인화된 설정, 장바구니 정보 등을 유지할 수 있음.
           2. 키는 클라이언트 측에 저장되므로 서버의 메모리나 데이터베이스에 부담을 주지 않음
           3. 쿠키는 HTTP 헤더에 포함되어 자동으로 전송되므로, 별도의 서버 측 세션 관리 없이 상태를 유지할 수 있음.
           4. 영구 저장 가능: 쿠키는 만료 시간을 설정할 수 있어, 브라우저를 닫거나 컴퓨터를 재부팅하더라도 일정 기간 동안 정보를 유지할 수 있음.

    단점
           1. 쿠키는 클라이언트 측에 저장되기 때문에, 악의적인 사용자가 쿠키를 조작하거나 탈취할 위험이 있음.
              따라서 중요한 정보는 쿠키에 직접 저장하지 않는 것이 좋음.
           2. 쿠키는 일반적으로 하나 당 최대 4KB까지의 데이터를 저장할 수 있음. 많은 데이터를 저장하는 것에는 한계가 있음.
           3. 쿠키는 브라우저에 의존하며, 사용자가 브라우저 설정을 통해 쿠키 저장을 거부할 수 있음. 이런 경우 쿠키를 활용한 상태 유지가 불가능해짐.
           4. 클라이언트가 서버로 요청을 보낼 때마다 쿠키가 함께 전송되므로, 쿠키 크기가 커질수록 네트워크 성능에 영향을 미칠 수 있음.
<hr>

# Cookie 구현 코드 
[cookie.zip](https://github.com/user-attachments/files/16683720/cookie.zip) (Intellij / Spring Boot / Gradle / zip 파일 다운 받으면 전체코드 다운가능)
```java
   package com.example.cookie.service;

import com.example.cookie.db.UserRepository;
import com.example.cookie.model.LoginRequest;
import jakarta.servlet.http.Cookie;
import jakarta.servlet.http.HttpServletResponse;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;

@Service
public class UserService {

    @Autowired
    private UserRepository userRepository;

    // cookie를 만드는 방법 1 (HttpServletResponse 사용)
    public void login1(
            LoginRequest loginRequest,
            HttpServletResponse httpServletResponse
    ) {
        var id = loginRequest.getId();
        var password = loginRequest.getPassword();

        var optionalUser = userRepository.findByName(id);

        // DB에 아이디가 존재하면
        if(optionalUser.isPresent()) {
            // userDto를 가져옴
            var userDto = optionalUser.get();

            // db에 있는 비밀번호와 입력받은 비밀번호가 같다면
            if(userDto.getPassword().equals(password)) {

                // 여기서부터 쿠키 세팅
                var cookie = new Cookie("authorization-cookie", userDto.getId()); // 편의성을 위해 userId로 쿠키를 설정하였는데, 실제 개발시는 다른 값으로 설정해주세요
                cookie.setDomain("localhost"); // 특정 도메인에서만 사용가능하게 (해당 코드는 로컬호스트로 설정)
                cookie.setPath("/"); // 주소설정
                cookie.setHttpOnly(true); // js에서 cookie 탈취 못하게 막는 보안코드 -> 필수!!
                cookie.setSecure(true); // Https에서만 쿠기가 사용되도록 설정 -> 마찬가지로 필수!!
                cookie.setMaxAge(-1); // -1은 연결된 동안만 사용 = 세션이 유지되는 동안만 사용

                // 응답에 쿠키를 추가
                httpServletResponse.addCookie(cookie);
            } else {
                throw new RuntimeException("Password Not Match");
            }
        } else {
            throw new RuntimeException("User Not Found");
        }
    }

// cookie를 만드는 방법 2 (HttpHeader 사용)
    public void login2(
            LoginRequest loginRequest,
            HttpServletResponse httpServletResponse
    ) {
        var id = loginRequest.getId();
        var password = loginRequest.getPassword();

        var optionalUser = userRepository.findByName(id);

        // DB에 아이디가 존재하면
        if(optionalUser.isPresent()) {
            // userDto를 가져옴
            var userDto = optionalUser.get();

            // db에 있는 비밀번호와 입력받은 비밀번호가 같다면
            if(userDto.getPassword().equals(password)) {

                // 여기서부터 쿠키 세팅
                var cookie = new Cookie("authorization-cookie", userDto.getId()); // 편의성을 위해 userId로 쿠키를 설정하였는데, 실제 개발시는 다른 값으로 설정해주세요
                cookie.setDomain("localhost"); // 특정 도메인에서만 사용가능하게 (해당 코드는 로컬호스트로 설정)
                cookie.setPath("/"); // 주소설정
                cookie.setHttpOnly(true); // js에서 cookie 탈취 못하게 막는 보안코드 -> 필수!!
                cookie.setSecure(true); // Https에서만 쿠기가 사용되도록 설정 -> 마찬가지로 필수!!
                cookie.setMaxAge(-1); // -1은 연결된 동안만 사용 = 세션이 유지되는 동안만 사용

                // 헤더에 쿠키를 추가
                HttpHeaders httpHeaders = new HttpHeaders();
                headers.add("Set-Cookie", cookie.toString());
            } else {
                throw new RuntimeException("Password Not Match");
            }
        } else {
            throw new RuntimeException("User Not Found");
        }
    }
```
<hr>

# JWT Token (JSON Web Token)
    정의 : JSON 객체를 사용하여 웹에서 사용자 정보를 인증하고 전달하기 위해 사용되는 토큰 기반의 인증방식

    형태(예시)  
          eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9. (헤더)
          eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.(페이로드)
          SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c(서명)

    구성 : JWT Token은 세 가지 구성으로 이루어지며 '.'을 기준으로 구분되어짐
    
           1. 헤더 : 토큰의 타입(JWT)과 해싱 알고리즘을 지정하는 정보를 담고 있음.
                  　 여기서 해싱알고리즘이란 후에 설명할 페이로드와 헤더를 조합하여 서명을 만들때 사용함
                    
           2. 페이로드 : 사용자 정보나 그 외 정보를 담고 있는 부분으로, JSON 형식으로 인코딩 됨.
                      　 이 정보는 보통 클레임이라고 부르며, 토큰의 발급자, 유효기간, 사용 ID 등의 정보가 포함됨.

           3. 서명 : 해싱알고리즘을 통해 헤더와 페이로드를 인코딩 한 후, 비밀키를 사용해 생성됨.
                     이 서명은 데이터의 무결성을 보장하며, 서버가 토큰을 검증할 때 사용함.
                        
                     여기서 무결성이란 데이터가 원래 의도된 상태에서 변경되지 않음을 의미함.
                     여기서 비밀키란 특정 데이터를 암호화하거나 서명할 때 사용하는 비밀로 유지되는 고유한 키 값을 의미함.
                     비밀키는 개발자가 직접 설정하거나, 키 관리 시스템(KMS), 라이브러리 등을 이용해 생성함.

    특징 
           1. 자체포함 : JWT는 필요한 모든 정보를 자체적으로 포함하고 있어, 서버는 별도의 상태를 유지하지 않고도 클라이언트를 인증할 수 있음        
           2. 확장성 : JWT는 매우 유연하여 페이로드에 다양한 클레임을 저장하여, 정보를 전달할 수 있음.                                       
           3. 무결성 검증 : 서명 부분을 통해 토큰이 변경되지 않았음을 검증할 수 있음.

    장점 
           1. 토큰 기반의 인증방식이므로, 서버 측에서 별도의 세션 저장소를 유지할 필요가 없음
           2. JSON 형식으로 인코딩되므로, 다양한 플랫폼 간에 쉽게 전송 및 구현가능
           3. 서명을 사용하여 무결성을 보장하므로, 토큰이 변조되었는지 여부를 쉽게 검증가능

    단점 
           1. JWT의 크기가 커질 경우, 네트워크 대역폭이 증가하게 됨
           2. JWT는 한 번 발급된 이후 내부 정보를 수정할 수 없으므로, 만료시간을 짧게 설정해야함
           3. JWT를 탈취당하면 해당 토큰을 사용한 모든 요청이 인증되므로, 보안에 위협이 됨.
              -> HTTPS와 같은 보안 프로토콜을 사용할 것을 추천

    주 사용처 
           사용자 인증(로그인) : 사용자가 로그인하면 서버는 JWT 토큰을 발급하고, 
           클라이언트는 이후 요청시 헤더에 토큰을 포함시켜 인증을 수행함
   ![image](https://github.com/user-attachments/assets/1f4fc82a-e492-480b-9603-dfc77d4ea11a)
   ![image](https://github.com/user-attachments/assets/29dd1707-f305-45a9-bb22-e4f962a9faf8)

   공식사이트 링크 : https://jwt.io/
<hr>

# JWT Token 구현 코드 
[jwt.zip](https://github.com/user-attachments/files/16675275/jwt.zip) (Intellij / Spring Boot / Gradle / JJWT 라이브러리 사용, zip 파일 다운 받으면 전체코드 다운가능 )
```java
package com.example.jwt.service;

import io.jsonwebtoken.ExpiredJwtException;
import io.jsonwebtoken.Jwts;
import io.jsonwebtoken.SignatureAlgorithm;
import io.jsonwebtoken.security.Keys;
import io.jsonwebtoken.security.SignatureException;
import lombok.extern.slf4j.Slf4j;
import org.springframework.stereotype.Service;

import java.time.LocalDateTime;
import java.time.ZoneId;
import java.util.Date;
import java.util.Map;

@Slf4j
@Service
public class JwtService {

    private static String secretKey = "JWTTokenForSpringBootTest123456789HelloWorld";

    // 토큰 발행
    public static String create(
            Map<String, Object> claims,
            LocalDateTime expiredAt
    ) {

        // 비밀키 생성
        var key = Keys.hmacShaKeyFor(secretKey.getBytes());
        var _expiredAt = Date.from(expiredAt.atZone(ZoneId.systemDefault()).toInstant()); // LocalDateTime을 Date 형식으로 변환


        // JWT Token 생성 (미리 만들어진 라이브러리를 사용한)
        return Jwts.builder()
                .signWith(SignatureAlgorithm.HS256, key) // H256 해시 알고리즘과 비밀키를 사용하여 서명 생성
                .setClaims(claims) // 페이로드에 claims 추가
                .setExpiration(_expiredAt) // 토큰 만료시간 설정
                .compact();
    }

    // 토큰 검증
    public static void validation(String token) {
        var key =  Keys.hmacShaKeyFor(secretKey.getBytes()); // 토큰을 만들때 사용한 비밀키를 가져옴

        // parser 생성
        var parser = Jwts.parser()
                .setSigningKey(key) // 서명을 읽기위한 비밀키 설정
                .build();
        try {
            // parser를 통해 token을 읽음
            var result = parser.parseClaimsJws(token);
            result.getBody().entrySet().forEach(value -> { // map 안에 저장된 key, value 값을 순차적으로 출력
                log.info("key : {}, value : {}", value.getKey(), value.getValue());
            });
        } catch (Exception e) { 
            if (e instanceof SignatureException) {
              // 이곳에 예외처리 코드를 작성
            } else if (e instanceof ExpiredJwtException) {
              // 이곳에 예외처리 코드를 작성
            } else {
              // 이곳에 예외처리 코드를 작성
            }
        }
    }
}
```




