# CPU 스케줄링
    CPU 스케줄링이란 운영체제가 프로세스들에게 공정하고 합리적으로 CPU 자원을 배분하는 것

    CPU 스케줄링은 컴퓨터의 성능과도 직결되기 때문에 매우 중요한 문제라고 할 수 있음

# 프로세스 우선순위
    프로세스에는 '입출력 집중 프로세스' 와 'CPU 집중 프로세스' 가 있음

    입충력 집중 프로세스는 실행 상태보다 입출력을 위한 대기 상태에 더 많이 머무르고,
    CPU 집중 프로세스는 대기 상태보다는 실행상태에 더 많이 머무름

![image](https://github.com/user-attachments/assets/f1ee8d22-db2d-461d-b0ec-6ba881816c92)

    입출력 집중 프로세스는 CPU에 잠깐만 머무르면 되기 때문에, CPU 집중 프로세스에 비해 프로세스 우선순위가 높음

![image](https://github.com/user-attachments/assets/14d6aa22-ac24-40ed-95e3-11e92ece93a2)

    운영체제는 프로세스의 우선순위를 PCB(Process Control Block)에 명시함

![image](https://github.com/user-attachments/assets/28ab9d05-e3b3-40d7-a76f-9e2dac1671d9)

# 스케줄링 큐
    PCB에 프로세스의 우선순위가 적혀있다고는 하지만 CPU가 다음번에 사용할 프로세스를 찾기 위해
    운영체제가 모든 프로세스의 PCB를 확인하는 것은 매우 비효율적인 작업임

    그래서 운영체제는 프로세스들에게 줄을 서서 기다릴 것을 요구하고,
    이 줄을 스케줄링 큐로 구현하고 관리함 (스케줄링에서 얘기하는 큐는 자료규조의 큐처럼 반드시 FIFO 구조는 아님)
    
![image](https://github.com/user-attachments/assets/45e54bee-331b-4e49-88b4-5cec2cec04b9)

# 스케줄링 큐의 종류
    스케줄링 큐에는 다양한 종류가 있는데 그 중 대표적인 큐로 준비 큐와 대기 큐가 있음

    준비 큐는 CPU를 이용하고 싶은 프로세스들이 서는 줄을 의미하고,
    대기 큐는 입출력장치를 이용하기 위해 대기에 접어든 프로세스들이 서는 줄을 의미함

    물론 프로세스들이 준비 큐에 줄을 섰다고 해도 반드시 줄을 선 순서대로 CPU를 사용하는 것은 아님
    앞서 설명한 프로세스 간의 우선순위까지 고려하여 CPU를 사용하게 됨 (마치 롯데월드 프리패스 권과 같달까...?)

![image](https://github.com/user-attachments/assets/94614e07-bb48-4a72-b75b-7f62796a8f34)

    대기 큐 또한 특정 프로세스의 입출력이 완료되어 완료 인터럽트가 발생하면,
    대기 큐에서 작업이 완료된 PCB를 찾고, 이 PCB를 준비 큐에 넣 뒤 대기 큐에서 삭제함

![image](https://github.com/user-attachments/assets/a8fa8bfe-d84b-472a-9298-7f53498f5d8a)
    
# 선점형과 비선점형 스케줄링
    선점형 스케줄링은 프로세스가 CPU를 비롯한 자원을 사용하고 있더라도
    운영체체가 자원을 강제로 빼앗아 다른 프로세스에 할당할 수 있는 방법

    따라서 특정 프로세스 실행 도중 더 급한 프로세스가 끼어들어도 
    더 급한 프로세스를 우선적으로 처리해주는 것이 가능함

![image](https://github.com/user-attachments/assets/1bc0dda5-4262-4c90-8da4-c52c0b3b0947)
    
    비선점형 스케줄링은 하나의 프로세스가 자원을 사용하고 있다면
    해당 프로세스가 종료되거나 스스로 대기 상태에 접어들기 전까지는 다른 프로세스가 끼어들 수 없는 방법

![image](https://github.com/user-attachments/assets/037bf720-0354-4c11-9094-c81093488a08)
    
