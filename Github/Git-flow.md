# Git-flow란?

- 소프트웨어의 소스코드를 관리하고 출시하기 위한 브랜치 관리 전략 중 하나

- Git-flow에서 사용하는 브랜치는 총 5가지로, <br>
  항상 유지되는 메인브랜치(Main, Develope)와 일정기간 유지되는 보조브랜치(Feature, Realease, Hotfix)로 나뉨.

  * Main<br> - 현재까지 만들어진 버전(코드)을 담고있는 브랜치

  * Develope<br> - 신기능 개발, 버그 수정 등을 하기 위한 Main 브랜치 복사 버전(코드)을 담고있는 브랜치

  * Feature<br> - 새로운 기능을 개발하기 위한 브랜치<br>
    &nbsp;&nbsp; Feature 브랜치에서 신기능 개발을 해보고 잘되면 Develope 브랜치에 merge

  * Realease<br> - 다음 버전을 준비하기 위한 브랜치<br>
    &nbsp;&nbsp; Develope 브랜치가 출시가능한 수준까지 개발되었을 때,<br>
    &nbsp;&nbsp; Main 브랜치에 merge 하기 전 여러가지 테스트 및 버그수정

  * Hotfix<br> - 출시 버전(Main 브랜치)에서 발생한 버그를 수정하는 브랜치<br><br>
    
    ![image](https://github.com/KYOUNGBEOM/STUDY/assets/112946948/820367b4-786c-4e5a-93e3-a565851f4369)

    참고자료 : [Git-flow 설명 영상](https://www.google.com)

