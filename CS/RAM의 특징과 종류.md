# RAM의 특징
- RAM에는 실행할 프로그램의 명령어와 데이터가 저장
- RAM은 컴퓨터 전원을 끄면 저장된 내용이 사라지는 '휘발성 저장 장치'임

# 보조기억장치
- 보조기억장치에는 SSD, CD-ROM, USB 메모리 등이 있음
- 보조기억장치는 대표적인 '비휘발성 저장 장치'임
- CPU는 보조기억장치에 직접적으로 접근할 수 없음

#### 결론적으로, 일반적으로 RAM은 '실행할 대상'을 저장하고, 보조기억장치에는 '보관할 대상'을 저장함
#### 따라서, CPU가 실행하고 싶은 프로그램이 보조기억장치에 있다면 이를 RAM에 복사하여 저장한 뒤 실행함

# RAM의 용량과 성능
- 만약 RAM의 용량이 작다면 보조기억장치에서 실행할 프로그램을 가져오는 일이 잦아져 실행시간이 길어짐

![image](https://github.com/user-attachments/assets/ca943728-85e0-4a14-b2d6-d6c38c379f6c)

- 반면 RAM의 용량이 크다면, 보조기억장치로부터 한 번에 많은 프로그램을 들고와서 실행시킬 수 있음

![image](https://github.com/user-attachments/assets/bd1db48b-da90-4ace-a897-a12dec83f6b4)

- 물론 그렇다고 해서 RAM의 용량에 비례하여 절대적인 프로그램 실행속도가 빨라지는 것은 아님 <br>
- 예를 들어, 실행시키고자 하는 프로그램이 100개 일때,<br>
  용량이 100인 RAM과 1000인 RAM 사이의 실행속도는 큰 차이가 없을것임

# RAM의 종류
- RAM의 종류는 크게 DRAM, SRAM, SDRAM, DDR SDRAM이 있음

- ### DRAM(Dynamic RAM)
  - 저장된 데이터가 동적으로 변하는 RAM을 의미함
  - DRAM은 시간이 지나면 저장된 데이터가 점차 사라짐 <br>
    따라서, DRAM은 데이터의 소멸을 막기 위해 일정 주기로 데이터를 재활성화 해야함
  - 이러한 단점에도 불구하고, 일반적으로 사용하는 RAM은 DRAM임 <br>
    이유는 소비 전력이 비교적 낮고, 저렴하고, 집적도가 높아 대용량으로 설계하기 좋기 때문임
    
- ### SRAM(Static RAM)
  - 저장된 데이터가 변하지 않는 RAM을 의미함
  - SRAM은 DRAM과 달리 시간이 지나도 저장된 데이터가 사라지지 않음 <br>
    따라서, 주기적으로 데이터를 재활성화할 필요가 없음 <br>
    또한, DRAM에 비해 일반적으로 속도도 더 빠름
  - 물론, 저장된 데이터가 사라지지 않는다고 해서 '비휘발성 메모리'인 것은 아님 <br>
    여타 RAM과 마찬가지로 전원이 꺼지면 저장된 내용이 날아감
  - 그럼에도 SRAM은 DRAM에 비해 소비 전력이 크고, 비싸며, 집적도가 낮기 때문에 잘 사용되지 않음 <br>
    그래서 '대용량으로 만들어질 필요는 없지만 속도가 빨라야하는 저장 장치'에 자주 사용됨(캐시 메모리)

![image](https://github.com/user-attachments/assets/612d2d86-56e9-410c-b051-4fee162a77e9)

- ### SDRAM(Synchronous Dynamic RAM)
  - 이름만 보면 오해하기 쉽지만, SDRAM은 SRAM과는 관계가 없음
  - SDRAM은 클럭 신호와 동기화된 발전된 형태의 DRAM임
  - 클럭 신호와 동기화 되었다는 것은 클럭 타이밍에 맞춰 CPU와 정보를 주고 받을 수 있음을 의미함 <br>
    즉, SDRAM은 클럭에 맞춰 동작하며 클럭마다 CPU와 정보를 주고받을 수 있는 DRAM임
    
- ### DDR SDRAM(Double Data Rate SDRAM)
  - 최근 가장 흔히 사용되는 RAM임
  - DDR SDRAM은 대역폭을 넓혀 속도를 빠르게 만든 SDRAM임 <br>
    여기서 대역폭이란 '데이터를 주고 받는 길의 넓이'를 의미함
  - SDR SDRAM은 한 클럭에 1 번씩 CPU와 데이터를 주고 받을 수 있는 RAM <br>
    DDR SDRAM은 한 클럭에 2 번씩 CPU와 데이터를 주고 받을 수 있는 RAM <br>
    DDR2 SDRAM은 한 클럭에 4 번씩 CPU와 데이터를 주고 받을 수 있는 RAM <br>
    DDR3 SDRAM은 한 클럭에 8 번씩 CPU와 데이터를 주고 받을 수 있는 RAM

![image](https://github.com/user-attachments/assets/5b8133e4-9240-4eb5-a70d-9cd48a844510)
![image](https://github.com/user-attachments/assets/a03f1d8d-248b-48dc-9c57-50a32d967c0d)

  
