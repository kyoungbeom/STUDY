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
[jwt.zip](https://github.com/user-attachments/files/16675275/jwt.zip) (Intellij / Spring Boot / Gradle / JJWT 라이브러리 사용, 전체 파일 다운 가능)
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




