# SQL Injection 이란?
    악의적인 사용자가 보안상의 취약점을 이용해, 임의의 SQL문을 주입하고 실행되게 하여 DB가 비정상적인 동작을 하도록 조작하는 행위를 의미함.
    
    Error based SQL Injection, Union based SQL Injection, Boolean based SQL Injection, Time based SQL Injection 등 다양한 공격기법이 있음.
    
    대응 방안으로는 입력 값에 대한 검증, Prepared Statement 구문 사용, Error Message 노출 금지, 웹 방화벽 사용 등의 방안이 있음.
