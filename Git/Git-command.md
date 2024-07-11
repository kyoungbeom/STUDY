# git init 
  - Git 저장소를 초기화하는 명령어
  - 명령어를 실행하면 현재 디렉토리 상에 '.git'이라는 하위 디렉토리가 생성됨
  - 즉, 'git init' 명령어는 Git을 사용할 수 있도록 해당 디레토리를 Git 저장소로 만듦.
  - git init --bare 생성할 폴더이름, 저장소를 초기화시키지만 워킹 디렉토리가 생성되지 않아 파일을 수정하거나 커밋할 수 없음. <br>
    오직 push, pull만 가능한 원격 저장소로서의 역할을 함

# git add 
  - 작업 디렉토리의 변경 내용을 스테이징 영역에 추가하는 명령어
  - 'git add 파일명'을 실행하면 해당 파일의 변경 내용이 스테이징 영역에 추가

# 스테이징 영역의 역할
1. 변경 사항의 준비 단계
    - 작업 디렉토리에서 파일을 수정하면 Git은 이 파일의 변경 사항을 추적
    - 이 변경 사항은 아직 스테이징 영역에 포함되지 않은 상태
    - git add 명령어를 사용하면, 작업 디렉토리의 변경 사항을 스테이징 영역에 추가할 수 있음

2. 커밋의 준비 상태
    - 스테이징 영역에 파일을 추가하면, 해당 파일들은 다음 git commit 명령어를 통해 실제로 저장소에 커밋될 준비가 된 상태
    - 즉, 스테이징 영역은 커밋할 변경 사항을 준비하는 공간으로, 필요한 파일들을 추가하고 정리하는 역할

3. 분리된 개념
    - 스테이징 영역은 작업 디렉토리와 실제 저장소(로컬 또는 원격) 사이에 위치하며,<br>
      작업 디렉토리의 변경 사항을 정리하고 명확히 구분하는 역할
    - 이는 변경 사항을 여러 단계로 분할하여 관리하고, <br>
      필요한 경우 변경 사항을 다시 수정하거나 취소할 수 있는 유연성을 제공

# git commit
  - 스테이징 영역에 있는 파일들의 변경 사항이 새로운 커밋으로 저장소에 영구적으로 기록하는 명령어
  - git commit 명령어를 사용하면 Git이 설정된 텍스트 편집기(기본적으로는 Vim)를 열어 커밋 메시지를 입력하도록 함
  - 메시지 작성 후 저장하면 해당 커밋이 완료
  - git commit -a = git add + git commit
  - git commit -m "내용" 의 형태로 입력하면, <br>
    스테이징 영역에 있는 변경 사항을 "내용" 이라는 메시지와 함께 새로운 커밋으로 기록가능
  - git commit -am "내용" 의 형태로 입력하면, <br>
    수정된 모든 파일(추적되지 않는 파일은 제외)을 준비한 다음 지정된 커밋 메시지와 함께 한꺼번에 커밋
  - 커밋을 통해 프로젝트의 변경 이력을 관리하고, 팀원들과 협업하며, <br>
    문제가 발생했을 때 이전 상태로 되돌릴 수 있는 강력한 기능을 제공

# git status
1. 추적 중인 파일과 변경된 파일 확인

    - git status를 실행하면, 현재 작업 디렉토리에 있는 파일들 중 Git이 추적하고 있는 파일과 그 변경 사항을 보여줌
    - 변경된 파일은 "Changes not staged for commit" 섹션에 나열

2. 스테이징 영역에 추가된 파일 확인
    - git add로 스테이징 영역에 추가된 파일들은 "Changes to be committed" 섹션에 나열
    - 이 섹션에 있는 파일들은 다음 git commit 명령어를 통해 커밋할 준비가 되었다는 것을 의미
  
# git config --global 
  - 시스템에서 Git 구성을 전역적으로 설정하는 데 사용되는 명령어
  - 설정은 머신의 모든 저장소에 적용
  - git config --global user.name "Your Name" 시스템의 모든 Git 저장소에 대한 글로벌 사용자 이름을 설정
  - git config --global merge.tool kdiff3 병합 과정에서 충돌이 발생했을 때, 충돌을 관리해주는 툴 (툴 설정 후 git mergetool 입력하여 사용)
    
# git log   
  - 현재 저장소의 커밋 기록을 검색하고 표시하는 명령어
  - git log -p를 사용하면 커밋과 커밋 사이의 소스상 차이를 확인가능
  - git log --branches --decorate --graph --oneline, <br>
     --branches: 모든 브랜치의 커밋을 보여줌 <br>
     --decorate: 해당 커밋 옆에 브랜치 이름, 태그 및 기타 참조를 추가 <br>
     --graph: 부모 커밋과 자식 커밋을 연결하는 선이 있는 그래프로 커밋 기록을 표시 <br>
     --oneline: 각 커밋을 한 줄에 표시하여 출력을 더 간결하고 읽기 쉽게 만들어줌
  - git log 브랜치명1..브랜치명2, 브랜치1에는 없고 브랜치2에는 있는 내용을 보여줌
  - gir reflog, 참조(HEAD나 브랜치)의 변경 이력을 보여주는 명령어로, <br>
    커밋, 리셋, 체크아웃 등의 작업을 할 때마다 기록되며, 잃어버린 커밋을 복구하거나 기록되지 않은 히스토리를 이해하는 데 매우 유용 
    

# git diff
  - 현재 스테이징된(changes staged for commit) 변경 사항과 아직 스테이징되지 않은(changes not staged for commit) 워킹 디렉토리의 변경 사항을 비교하는 명령어
  - git diff 커밋 아이디1..커밋 아이디2 의 형태로 입력하면, 각 id에 해당하는 커밋 사이의 소스상 차이 확인가능

# git reset
  - git에서 커밋 기록을 조작하거나 작업 트리의 상태를 변경하는 데 사용하는 명령어
  - git reset 커밋 아이디 --soft (소프트 리셋), 변경 사항을 그대로 유지한 채로 이전 커밋을 취소하고 변경 사항은 스테이징 영역에 남아있음 
  - git reset 커밋 아이디 (미디엄 리셋), 변경 사항을 워킹 디렉토리에 보존하되, 스테이징 영역에서 취소
  - git reset 커밋 아이디 --hard (하드 리셋), 변경 사항을 스테이징 영역 및 워킹 디렉토리에서 모두 취소
  - 하드리셋을 사용할 때는 변경 사항을 되돌릴 수 없으므로 주의가 필요
  - 원격 저장소에 이미 push 한 커밋을 reset 하면 협업과정에서 문제가 생기므로 매우 주의

# git branch
  - 브랜치를 나열, 생성, 삭제 하는데 사용되는 명령어
  - git branch, 저장소의 모든 브랜치를 나열
  - git branch 브랜치명, 현재 브랜치를 복사한 새로운 이름의 브랜치가 생성
  - git branch -d 브랜치명, 지정된 브랜치를 삭제
  - git branch -m 새로운 브랜치명, git에는 기존 브랜치에 대한 이름 변경 권한이 없음 <br>
    따라서 원하는 이름으로 새 브랜치를 만들고 기존 브랜치를 삭제함
  - git checkout 브랜치명, 입력한 브랜치명으로 브랜치 이동
  - git checkout -b 브랜치명 = git branch 브랜치명 + git checkout 브랜치 (브랜치 생성 + 작업 브랜치 이동)

# git merge
  - 여러 개발 히스토리를 하나로 합치는 작업으로, 브랜치를 병합 시킬때 사용하는 명령어
  - git merge 브랜치명, 현재 위치한 브랜치에 브랜치명을 병합시킴
  - Fast forward
    
    - hotfix 브랜치가 가리키는 C4 커밋이 C2 커밋에 기반한 브랜치이기 때문에 브랜치 포인터는 Merge 과정 없이 그저 최신 커밋으로 이동 <br>
      이런 Merge 방식을 “Fast forward” 라고 부름. 
      ![basic-branching-5](https://github.com/KYOUNGBEOM/STUDY/assets/112946948/79775c7e-114a-4aea-9c52-b43391d3c1d3) <br>

  - 3-way Merge

    - 각 브랜치가 가리키는 커밋 두 개와 공통 조상 하나를 사용하여 병합하는 것을 3-way Merge 라고 함
    - 단순히 브랜치 포인터를 최신 커밋으로 옮기는 게 아니라 <br>
      3-way Merge 의 결과를 별도의 커밋으로 만들고 나서 해당 브랜치가 그 커밋을 가리키도록 이동시킴
      ![basic-merging-2](https://github.com/KYOUNGBEOM/STUDY/assets/112946948/4e677add-35bb-4ac3-a747-0cff9d2219d7)

# git stash
  - 작업 디렉토리에서 커밋할 준비가 되지 않은 변경 사항을 일시적으로 저장하는 명령어
  - git stash list, 모든 저장된 변경 사항 목록을 표시
  - git stash apply, 가장 최근의 stash가 작업 디렉토리에 다시 적용
  - git stash drop, 가장 최근의 stash 삭제
  - git stash pop = git stash apply + git stash drop (stash 작업 디렉토리 적용 + 가장 최근 stash 삭제)
  - git stash clear, 저장된 모든 stash 삭제

# git 원격 저장소 
  - git remote add 원격이름 원격url, ( 예시 : git remote add origin https://github.com/username/repository.git ) <br>
      - 예시 명령어는 현재 로컬 저장소에 origin이라는 이름으로 GitHub 저장소를 추가하고, <br>
         origin이라는 이름을 사용하여 원격 저장소와 상호작용할 수 있게함
  - git remote -v, 현재 로컬 저장소에 추가된 모든 원격 저장소의 목록과 URL 출력
  - git remote remove 원격이름, 연결된 원격 저장소를 삭제
  - git push, 로컬 저장소의 내용을 연결한 원격 저장소에 저장
  - git push --set--upstream 원격이름 브랜치이름, 설정한 브랜치에서 push를 하면 자동으로 설정한 원격 저장소로 내용을 push 

    
Git-Book(manual) : https://git-scm.com/book/en/v2 
