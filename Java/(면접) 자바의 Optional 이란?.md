# Optional 이란?
    Java 8에서 도입된 기능으로, 주로 NullPointerException을 방지하고 보다 명시적으로 null을 처리하는 데 사용된다. 

    기본적으로 Optional은 값이 있을 수도, 없을 수도 있는 상황을 표현할 수 있다. 
    
    예를 들어 isPresent(), orElse(), ifPresent()와 같은 메서드를 사용해, 
    값이 존재하지 않을 때의 기본값 설정이나, 값이 있을 때의 처리 로직을 간단하게 구현할 수 있다.
    
    즉, Optional 클래스를 사용하면 개발자가 일일이 null 체크를 하지 않아도 되도록 한다. 

    이를 통해 코드의 가독성과 안전성을 높이고, null 관련 에러를 효과적으로 방지할 수 있는 점이 Optional의 가장 큰 장점이다
