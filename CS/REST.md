# REST(Represetational State Transfer, 자원의 상태 전달) 
    1. 클라이언트와 서버가 독립적으로 분리되어 있어야 함
       클라이언트는 서버의 내부 구조나 데이터베이스에 대해 알 필요가 없고, 서버 역시 클라이언트에 대한 정보를 몰라도 
    
    2. 요청에 대해 클라이언트의 상태가 서버에 저장되지 않음 (Stateless)
    
    3. 클라이언트가 캐시를 통해 응답을 재사용할 수 있어야 함
    
    4. 클라이언트와 서버사이에 방화벽, 게이트웨이, 프록시 등 다계층 형태를 구성할 수 있어야 함
    
    5. 클라이언트와 서버는 독립적으로 개선될 수 있어야 함
    
       즉, 서버의 인터페이스(URI, HTTP 메소드 등)는 일관성이 있어야 하며, 
       이를 통해 클라이언트와 서버가 서로 독립적으로 발전가능 (인터페이스 일관성)

# 인터페이스 일관성
  인터페이스 일관성이 잘 지켜졌는지에 따라 REST를 잘 사용했는지 판단가능
    
       1. 자원식별
          - 웹 기반 REST에서는 리소스에 접근할 때 URI를 사용
            EX). https://www.github.com/kyoungbeom/1 -> Resource : kyoungbeom / 식별자 : 1

       2. 메세지를 통한 리소스 조작
          - 리소스 타입을 알려주기 위해서 header 부분에 content-type을 통해서 어떠한 타입인지를 지정
          - 이를 통해 서버는 클라이언트가 보내는 데이터의 타입을 이해

       3. 자기서술적 메세지
          - 요청하는 데이터가 어떻게 처리되어져야 하는지 충분한 데이터를 포함해야함
          - HTTP 기반의 REST에서는 메소드(GET, POST, PUT, DELETE)와 헤더 정보 정보로 이를 표현

       4. 클라이언트 요청에 대한 데이터만 내리는 것이 아닌 관련된 리소스에 대한 Link 정보까지 포함해야 함
          
          EX). 요청 URI : GET /posts/1 
               서버 응답 : 
               
               {
                  "id": 1,
                  "title": "REST API 이해하기",
                  "content": "REST API는...",
                  "author": "홍길동",
                  "links": {
                     "author": "/authors/1",
                     "comments": "/posts/1/comments",
                     "related_posts": "/posts?tag=API"
                   }    
               }

       위 조건들이 잘 갖추어진 경우 REST ful 하다고 말하고 이를 REST API라고 부름
            
  
