## Git , Github

**버전 관리가 필요한 이유**

- 개발자 간의 협업을 위해 전체 개발 소스를 공유하면서 개발 파트를 나눌 수 있고 가튼 모듈을 개발하더라도 소스를 공유하며 개발하기 위한 목적

### Git

`버전 관리를 위한 [소프트웨어]`

- 오픈 소스 버전 관리 시스템(VCS : Version Control System)
- 로컬에서 버전 관리
- 소프트웨어 개발 및 소스 코드 관리에 사용

### Github

`git으로 저장되어 원격전송된 내역들이 저장되는 공간을 제공하는 [서비스]`

- Git Repository를 위한 웹 기반 호스팅 서비스
- 클라우드 서버를 사용해서 로컬에서 버전 관리한 소스코드를 업로드하여 공유 가능
- 분산 버전 제어, 액세스 제어, 소스 코드 관리, 버그 추적, 기능 요청 및 작업 관리를 제공
  <br/>

**Git의 workflow**
![workflow of git](https://git-scm.com/book/en/v2/images/reset-workflow.png)

### Git 명령어

1. 새로운 저장소 생성<br/>
   `$ git init` : .git 하위 디렉토리 생성
   <br/>
2. 저장소 복제/다운로드 (clone)<br/>
   `$ git clone <https:.. URL>` : 기존 소스 코드 다운로드/복제<br/>
   `$ git clone /로컬/저장소/경로` : 로컬 저장소 복제<br/>
   `$ git clone 사용자명@호스트:/원격/저장소/경로` : 원격 서버 저장소 복제
   <br/>
3. 추가 및 확정 (commit)<br/>
   `$ git add <파일명>` : 커밋에 단일 파일의 변경 사항을 포함(인덱스 추가상태)<br/>
   `$ git add-A` : 커밋에 파일의 변경 사항을 한번에 모두 포함<br/>
   `$ git commit -m "커밋 메시지"` : 커밋 생성 (실제 변경 사항 확정)<br/>
   `$ git status` : 파일 상태 확인
   <br/>
4. 가지치기 작업 (branch)<br/>
   `$ git branch` : 브랜치 목록<br/>
   `$ git branch <브랜치이름>` : 새 브랜치 생성 (local)<br/>
   `$ git checkout -b <브랜치이름>` : 브랜치 생성 & 이동<br/>
   `$ git checkout master` : .git 하위 디렉토리 생성<br/>
   `$ git branch -d <브랜치이름>` : 브랜치 삭제<br/>
   `$ git push origin <브랜치이름>` : 생성한 브랜치를 원격 서버에 전송<br/>
   `$ git push -u <remote> <브랜치이름>` : 새 브랜치를 원격 저장소로 push<br/>
   `$ git pull <remote> <브랜치이름>` : 원격에 저장된 git 프로젝트의 현재 상태를 다운 + 현재 위치한 브랜치로 merge
   <br/>
5. 변경 사항 발생 (push)<br/>
   `$ git push origin master` : 변경사항 원격 서버에 업로드<br/>
   `$ git push <remote> <브랜치이름>` : 커밋을 원격 서버에 업로드<br/>
   `$ git push -u <remote> <브랜치이름>` : 커밋을 원격 서버에 업로드<br/>
   `$ git remote add origin <등록된 원격 서버 주소>` : 클라우드 주소 등록 및 발행(git에게 새로운 원격 서버 주소 알림)<br/>
   `$ git remote remove <등록된 클라우드 주소>` : 클라우드 주소 삭제
   <br/>
6. 갱신 및 병합 (merge)<br/>
   `$ git pull` : 원격 저장소의 변경 내용이 현재 디렉토리에 가져와지고(fetch) + 병합(merge)<br/>
   `$ git merge <다른 브랜치이름>` : 현재 브랜치에 다른 브랜치의 수정사항 병합<br/>
   `$ git add <파일명>` : 각 파일을 병합할 수 있음<br/>
   `$ git diff <브랜치이름><다른 브랜치이름>` : 변경 내용 merge 전에 바뀐 내용을 비교할 수 있음
   <br/>
7. 태그작업 (tag)<br/>
   `$ git log` : 현재 위치한 브랜치 커밋 내용 확인 및 식별자 부여됨
   <br/>
8. 로컬 변경사항 작업 (return)<br/>
   `$ git checkout --<파일명>` : 로컬의 변경 사항을 변경 전으로 되돌림<br/>
   `$ git fetch origin` : 원격에 저장된 git 프로젝트의 현 상태를 다운
