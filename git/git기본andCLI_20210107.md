# Git

버전을 통해 코드를 관리하는 도구



## SCM & VCS

* SCM(Source Code Management) : 코드관리
* VCS(Version Control System) : 버전 관리



## Git 명령어

> Git은 **폴더 단위**로 프로젝트/코드를 관리

### 1. `git init`

* initialize,initiate : git 으로 코드 관리를 시작하겠다 선언하는 것
  1. `(master)`라는 표시가 프롬프트에 표시됨
  2. `.git`폴더가 생성됨(`ls -a`:숨김폴더 까지 모두 표시)



### 2. `git status`

**가장 중요한 명령어**

* git의 상태를 출력하는 명령어

  1. `git init`직후

  ```
  On branch master
  
  No commits yet
  
  nothing to commit (create/copy files and use "git add" to track)
  ```

  * No commits yet : 아직 commit이 없다(버전==스냅샷==특정상태==저장)
  * nothing to commit : commit 할게 없다.

  

  2. `a.txt`파일 추가후

  ```
  No commits yet
  
  Untracked files:
    (use "git add <file>..." to include in what will be committed)
          a.txt
  
  nothing added to commit but untracked files present (use "git add" to track)
  
  ```

  * untracked files : 추적되지 않은 파일이 있어요 (어떤 파일)
  * nothing added to commit but untracked files present : 커밋할 파일은 없지만, 추적되지 않는 파일은 있다.

  3. `git add a.txt`이후

  ```
  On branch master
  
  No commits yet
  
  Changes to be committed:
    (use "git rm --cached <file>..." to unstage)
          new file:   a.txt
  
  ```

  * changes to be committed : commit될 준비가 된 파일이 있음

  4. `git commit -m 'first commit'`이후

  ```
  On branch master
  nothing to commit, working tree clean
  
  ```

  * nothing to commit : commit 할 게 없음
  * working tree(directory) clean 



### 3. `git add [파일명]`

git이 스냅샷을 찍기 위해 추적하는 리스트에 파일을 추가한다.



### `git commit -m '[커밋 메시지]'`

git을 통해 스냅샷을 찍음(==버전을 만듬, 현재 상태를 저장)

* `-m`:message 줄임말

  1. 언제 찍었는지
2. 누가 찍었는지
  3. 메시지
4. commit hash (commit을 구분하기 위한 ID라고 생각,random하게 들어옴)

---

### `git config` commiter 설정

commit 한 사람의 정보를  넣어줘야 함

* `git config --global user.name '사용자 이름'`
* `git config --global user.email '사용자 이메일'`햣 



### `git log`

git 으로 지금까지 저장된 커밋들의 로그를 출력

* `git log --oneline` : 한 줄로 커밋을 출력
* `git log --[숫자]` : 입력된 숫자만큼 역순으로 출력(가장 최신 커밋부터)



---

# CLI

Command Line Interface(명령줄 인터페이스)

# GUI vs CLI

* GUI(Graphic User Interface) : 일반적(일반인)으로 컴퓨터를 다룬 방식(graphic 중심)
  * 마우스 중심
* CLI : 개발자들이 다루는 방식
  * 명령어 중심



## 명령어

폴더 == 디렉토리

*  `ls`(list) :해달 폴더(디렉토리) 내용출력
*  `pwd`(print working directory) : 현재 위치 출력
*  `cd[폴더명]`(change directory) : 폴더를 변경
   * `..`:상위폴더
   * `.`:현재폴더
   * `/`:루트 폴더
   * `~`: 홈 폴더
   * `Tab`:자동 완성
   * `cd`뒤에 아무것도 안치면 컴퓨터는 `~`가 생략되었다고 생각
*  `mkdir [폴더명]`(make directory) : 폴더 생성
*  `rm -r[폴더명]`(remove recursively, 계속 끝까지 아무것도 안나올 때 까지) : 폴더 삭제 
*  `touch [파일명]`: 파일 생성
*  `rm[파일명]`(remove): 파일 삭제



# 기초 명령어

## (1)`pwd`

* `pwd`(print working directory) :현재 폴더의 경로
* `~`(home directory) : 홈 디렉토리(git bash 처음 열면 나오는 기본 폴더)



## (2)`ls`

* `ls`(list): 내용물을 출력(list)



## (3)`cd [폴더명]`

* `cd`(change directory) : 폴더를 변경
* `cd ..`: 상위 폴더로 이동
* `cd .` : 현재 폴더로 이동



## (4) `mkdir [폴더명]`

* `mkdir`(make directory) : 폴더를 생성



## (5)`rm [파일명]`

* `rm`(remove) : 파일을 삭제



## (6) rm -r [폴더명]

* `-r`: recursively(재귀적으로) 폴더를 삭제



## (7) touch [파일명]

* `touch` : 파일생성



## (8) `cp [파일명]  [위치]`

* `cp`(copy) : 파일 복사



## (9) `cp -r [폴더명] [위치]`

* 폴더를 복사



## (10)`mv [파일/폴더명] [바꿀파일/폴더명]`

* `mv`(move) : 파일/폴더명 변경
* `mv [파일/폴더명] [위치]`: 파일 또는 폴더를 이동
