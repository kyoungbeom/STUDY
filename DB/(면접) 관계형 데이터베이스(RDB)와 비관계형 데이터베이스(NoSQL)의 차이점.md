# 1. 데이터 모델

### 관계형 데이터베이스    
    데이터가 테이블 형식으로 구조화되어 있으며, 각 테이블은 행과 열로 구성됨. 
    각 행은 레코드를 나타내고, 열은 속성을 나타냄. 관계를 정의하기 위해 외래 키를 사용함.
    
### 비관계형 데이터베이스
    데이터가 비구조적 또는 반구조적 형태로 저장됨. 
    JSON, XML, 키-값 쌍 등 다양한 형식을 지원하며, 데이터 모델이 유연함.

# 2. 스키마

### 관계형 데이터베이스
    스키마가 고정되어 있으며, 데이터가 삽입되기 전에 반드시 정의되어야 함. 

### 비관계형 데이터베이스 
    스키마가 유연하여, 데이터 형식이 일정하지 않아도 됨. 
    새로운 데이터 형식이 추가되더라도 기존 데이터에 영향을 미치지 않음.

# 3. 쿼리 언어

### 관계형 데이터베이스
    SQL(Structured Query Language)을 사용하여 데이터를 조회, 삽입, 수정, 삭제함. 쿼리가 강력하고 복잡한 연산을 지원함.
    
### 비관계형 데이터베이스
    다양한 쿼리 언어와 API를 사용함. 일반적으로 SQL보다 간단하며, 특정 데이터 모델에 맞춰 최적화되어 있음.
    대신, 복잡한 쿼리를 처리하기 어려울 수 있음.

# 4. 트랜잭션 처리

### 관계형 데이터베이스 
    ACID(Atomicity, Consistency, Isolation, Durability) 속성을 지원하여 강력한 트랜잭션 처리가 가능함. 데이터 무결성이 중요.

### 비관계형 데이터베이스 
    BASE(Basically Available, Soft state, Eventually consistent) 모델을 따르는 경우가 많아, 일관성보다는 가용성을 우선시함.

# 5. 확장성

### SQL 
    수직 확장(서버 성능을 높이는 방식)이 일반적이며, 대규모 데이터 처리에 한계가 있을 수 있음.
### NoSQL 
    수평 확장(서버를 추가함으로써 처리 능력 향상)이 용이하여 대규모 데이터와 높은 트래픽을 처리하는 데 적합함.
### 더 알아보기
    복잡성 
    SQL 데이터베이스 클러스터링은 설정과 유지 관리가 더 복잡할 수 있음. 
    NoSQL은 수평 확장에 최적화되어 있어 보통 더 쉽게 확장이 가능함.

    데이터 모델 
    SQL 데이터베이스는 스키마가 엄격하고, 관계형 모델에 기반하기 때문에 데이터의 정합성을 유지하는 데 강점을 가지지만, 이러한 특성으로 인해 수평 확장이 어렵거나 비효율적일 수 있음. 
    반면 NoSQL은 유연한 데이터 모델을 제공하여 수평 확장이 용이합니다.

    성능
    대규모 트래픽이나 데이터를 처리할 때 NoSQL은 일반적으로 더 높은 성능을 제공함. 
    SQL에서는 조인 연산이 성능을 저하시킬 수 있는데, 이는 NoSQL에서는 덜 발생함.
    
# 6. 사용 사례

### 관계형 데이터베이스
    금융, ERP 시스템 등 데이터 무결성이 중요한 경우에 적합.

### 비관계형 데이터베이스
    소셜 미디어, IoT, 실시간 분석 등 유연성과 확장성이 중요한 경우에 적합.   
    Redis, MongoDB 등등
