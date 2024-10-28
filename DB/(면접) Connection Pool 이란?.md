# Connection Pool
    Client의 요청에 따라 각 Application의 Thread에서 DB에 접근하기 위해서는 Connection이 필요함. 

    여기서, 요청이 올 때마다 Connection을 생성하는 방식은, 연결량이 많을 때 서버에 과부하가 걸리게 되는 현상이 발생함.
    
    하지만, Connection을 미리 만들어 Pool에 저장하면 이러한 현상을 방지할 수 있음.
    이것을 바로 Connection Pool 이라고 함

    Connection Pool을 사용하면, 생성 및 소멸에 대한 시간 소요가 없어지기 때문에 효율적이고, 
    한 번에 사용할 수 있는 커넥션 수가 제어되어 Application이 쉽게 죽지 않음.
