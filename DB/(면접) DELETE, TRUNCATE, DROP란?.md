## 1. DELETE
- **데이터 삭제 방식**: 데이터를 한 행씩 삭제하거나, 원하는 조건을 걸어 특정 데이터 여러 개를 삭제할 수 있음.
- **롤백 가능성**: 가능.
- **테이블 용량**: 삭제된 공간이 남아있어, 용량이 유지됨.
- **테이블 구조**: 테이블 구조 유지.

---

## 2. TRUNCATE
- **데이터 삭제 방식**: 테이블의 모든 데이터를 한 번에 삭제함.
- **롤백 가능성**: 트랜잭션 로그를 최소화 하므로, 불가능.
- **테이블 용량**: 삭제 후 공간이 해제되어, 용량이 줄어듬.
- **테이블 구조**: 테이블은 유지되지만, 데이터가 초기화(데이터 삭제 + 공간 해제)됨.

---

## 3. DROP
- **데이터 삭제 방식**: 테이블 자체를 삭제함.
- **롤백 가능성**: 불가능.
- **테이블 용량**: 모든 객체가 삭제됨.
- **테이블 구조**: 테이블과 그와 관련된 모든 객체(데이터, 인덱스 등)가 삭제됨.
