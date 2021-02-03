# Git

코드 관리 도구



## SCM & VCS

> Git은 **버전**을 통해 **코드를 관리**하는 독

* SCM (Source Code Management) : 코드 관리
  * 프로그램 (소스) 코드로 컴퓨터에게 명령 (Java -> Computer)
* VCS (Version Control System) : 버전 관리



## Git 명령어

Git은 **폴더 단위**로 코드를 관리



### (1) `git init`

특정 폴더(저장소, 프로젝트)에서 git을 시작 == 특정 폴더를 git으로 관리하기 시작

```shell
$ git init
Initialized empty Git repository in C:/Users/Student/test/.git
```

1.  `(master)`
2. `.git` 폴더가 생성
3. `.git` 폴더 삭제 시, git 관리 중지(git을 삭제)



### (2) `git status`

git의 현재 상태를 출력

* 최초 상태 (파일 없음)

``` shell
$ git status

On Branch master

No commits yet
-> 아직 버전이 없다.

nothing to commit (create/copy files and use "git add" to track)
-> 할 게 없다.
```



* 파일 생성 (`touch a.txt`)

``` 
On branch master

No commits yet

Untracked files
	(use "git add <file>..." to include in what will be committed)
	      a. txt
-> 추적되지 않는 파일
    (git add <특정파일>을 해줘, 버전(스냅샷)에 포함시키고 싶으면)
    
nothing added to commit but untracked files present (use "git add" to track)
-> 아직 commit 할 수 없다. 추적되지 않는 파일이 있다. (add 해라)
```



* `git add a.txt` 명령어 실행 후,

```
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
  		new file:   a.txt        
-> 버전으로 commit 할 변화가 있다. (== commit 할 수 있다.)
```



* `git commit` 실행 후,

``` 
On branch master
nothing to commit, working tree clean
-> 할 게 없다.
```



* `a.txt` 에 내용 추가 ('hi')

``` 
Changes not staged for commit:
   (use "git add <file>..." to update what will be committed)
   (use "git restore <file>..." to discard changes in working directory)
   		 modified:  a.txt
   		 
 no changes added to commit (use "git add" and/or "git commit -a")
```







### (3)`git add [파일명]`

commit을 위한 staging area에 파일 추가



### (4) `git commit -m "커밋 메세지"`

특정 상태를 스냅샷으로 찍어 버전을 만듬

	1. 누가 찍었는지(author)
 	2. 언제 찍었는지(date)
 	3. 어떤 내용을 찍었는지(message)

* 최초 `git commit` 시

```
Author identity unknown
-> 작성자의 신원을 모르겠다.
*** Please tell me who you are.
-> 니가 누군지 말해달라.
Run
-> 아래의 명령어를 실행해달라.
  git config --global user.email "you@example.com"
  git config --global user.name "Your Name"
 
to set your account's default identity.
Omit --global to set the identity only in this repository.

fatal: unable to auto-detect email address (got 'student@M301INS.(none)')

```



### (5) `git log`

지금까지 기록된 Commit (==버전 ==스냅샷)을 출력

* `git log --oneline` : 한 줄로 출력



### (6) `git diff [파일명]`

commit된 버전과 현재 상태의 차이를 출력



### (7) `git remote`

원격 저장소 정보를 출력

* `git remote add [이름] [주소]`
  * `git remote add origin http://github.com/yewon-kim96/test.git`

* `git remote -v` : verbose 모드



### (8) `git push [이름] [브랜치]`

* `git push origin master`



---

### (9)  `git config`

코드 관리 (버전) 주체가 누군지 설정

* `git config --global user.email [여러분의 이메일]` : 이메일을 조회/설정
* `git config --global user.name [여러분의 이름]` : 이름을 조회/설정







