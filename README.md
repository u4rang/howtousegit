# How to use git by CLI
This repository is to explain how to use git by cli.

----

# 용어 정리

|                용어                 | 설명                                                         |
| :---------------------------------: | :----------------------------------------------------------- |
|    워킹트리<br />(Working Tree)     | - 일반적인 작업이 일어나는 곳<br />- 사용자가 파일과 하위 디렉토리를 만들고 작업 결과물을 저장하는 위치 |
| 로컬저장소<br />(Local Repository)  | - ```$git init``` 명령어으로 생성되는 ```.git``` 디렉토리<br />- git 디렉토리, commit 으로 생성되는 정보 저장 |
| 원격저장소<br />(Remote Repository) | - 로컬 저장소를 업로드하는 곳<br />- GitHub 의 저장소<br />- 사용목적<br />    - 안정성<br />    - 협업 가능 |
|             Git 저장소              | - git 명령어로 관리하는 디렉토리 전체<br />- 좁은 의미로는 로컬저장소를 의미, 넓은 의미로는 워킹트리 |



# ```git``` 명령어

## ```git init``` 명령어

현재 디렉토리를 Git이 관리하는 프로젝트 디렉토리(=working directory)로 설정하고 그 안에 레포지토리(.git 디렉토리) 생성 한다.

```shell
$ git init
```

# ```git config``` 명령과  옵션 설정

|       옵션       | 설명                                    | 우선순위 |
| :--------------: | --------------------------------------- | :------: |
|    지역 옵션     | - 현재 Git 저장소에서만 유효한 옵션     |    1     |
|    전역 옵션     | - 현재 PC의 사용자에게만 유효한 옵션    |    2     |
| 시스템 환경 옵션 | - 현재 PC의 전체 사용자에게 유효한 옵션 |    3     |

```shell
# 지역 옵션
# 지정한 지역 옵션의 내용 확인
$ git config --local <옵션명>

# 지정한 지역 옵션의 값 설정
$ git config --local <옵션명> <설정값>

# 지정한 지역 옵션의 값 삭제
$ git config --local --unset <옵션명>

# 전역 옵션
# 지정한 전역 옵션의 내용 확인
$ git config --global <옵션명>

# 지정한 전역 옵션의 값 설정
$ git config --global <옵션명> <설정값>

# 지정한 전역 옵션의 값 삭제
$ git config --global --unset <옵션명>

# 시스템 환경 옵션
# 지정한 시스템 환경 옵션의 내용 확인
$ git config --system <옵션명>

# 지정한 시스템 환경 옵션의 값 설정
$ git config --system <옵션명> <설정값>

# 지정한 시스템 환경 옵션의 값 삭제
$ git config --system --unset <옵션명>

# 현재 프로젝트의 모든 옵션 확인
$ git config --list
```

전역 옵션의 user.name 과 user.email 에 대한 값을 확인하는 내용이다.

```shell
~/DEV/howtousegit main*
$ git config --global user.name # 전역 옵션의 user.name 확인
u4rang

~/DEV/howtousegit main*
$ git config --global user.email # 전역 옵션의 user.email 확인
u4rang@gmail.com
```

git 기본 에디터를 VS Code 로 설정하는 내용이다.

```shell
~/DEV/howtousegit main*
$ code --version 
1.24.1
24f62626b222e9a8313213fb64b10d741a326288
x64

~/DEV/howtousegit main*
$ git config --local core.editor

~/DEV/howtousegit main*
$ git config --global core.editor

~/DEV/howtousegit main*
$ git config --system core.editor

~/DEV/howtousegit main*
$ git config --system core.editor "code --wait"

~/DEV/howtousegit main*
$ git config --system core.editor
code --wait
```

## ```git config alias.[alias] [git 명령어]``` 명령어

길이가 긴 명령어에 대해 Alias 를 붙여 이후로 Alias로 해당 명령어를 실행 하도록 설정한다. 다음은 ```git log``` 명령어에 대해 다음과 같이 aliasing 하여 타이핑 및 보기 쉽게 하는 예제 이다.

```shell
$ git config alias.history 'log --pretty=oneline'

$ git config --global alias.l "log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr)%C(bold blue)<%an>%Creset' --abbrev-commit"
```

## ```git add``` 명령어

파일을 staging area 에 추가한다.

```shell
$ git add <파일명1> <파일명2> ...
```

## ```git add --all``` 명령어

```git add``` 명령어와 동일하게 파일을 staging area 에 추가한다. 차이점은 ```git add --all``` 명령어는 변경된 tracked 상태의 파일과 untracked 상태의 파일을 staging area 에 추가하기 때문에 변경 내역을 commit 전 branch를 이동할 때 유용하다.

```shell
$ git add --all
```

## ```git reset [파일명]``` 명령어

staging area영역에 있는 파일을 staging area영역에서 제외한다. (언스테이징) 워킹트리의 내용은 변경되지 않는다. 

```shell
$ git reset <파일명>
```

## ```git reset [옵션] [commit id]``` 명령어

branch의 작업 영역에 대해 `commit id`  기준으로 변경 한다. 옵션에 따라 Working Directory와 staging area영역, Repository 가 각각 달라진다.

```shell
$ git reset --hard aese
```

### reset 옵션에 따른 작업 영역의 변화

| 옵션  | Working Directory | Staging Area | Repository |                   설명                   |
| :---: | :---------------: | :----------: | :--------: | :--------------------------------------: |
| soft  |      안바뀜       |    안바뀜    | HEAD 이동  |  HEAD가 특정 Commit 을 가리키도록 이동   |
| mixed |      안바뀜       |     바뀜     | HEAD 이동  |  staging aread 도 특정 Commit처럼 리셋   |
| hard  |       바뀜        |     바뀜     | HEAD 이동  | Working Directory도 특정 commit처럼 리셋 |

## ```git commit``` 명령어

staging area 에 있는 파일을 commit 한다.

```shell
$ git commit
```

## ```git commit -m "commit message"```  명령어

staging area 에 있는 파일을 commit message와 함께 commit 한다.

```shell
$ git commit -m "commit message"
```

## ```git commit -a``` 명령어

```git add``` 명령어를 생략하고 바로 commit 하는 경우 사용한다. 변경된 파일과 삭제된 파일은 staging area 단계를 지나 commit 된다. 단, untracked 파일은 commit 되지 않는다.

```shell
$ git commit -a
$ git commit --all
```

## ```git push [-u] [원격저장소alias] [branch 명]``` 명령어

현재 branch에서 새로 생성한 commit 을 원격저장소에 업로드한다. -u 옵션으로 branch의 upstream을 등록할 수 있다. 1회 등록 후 ```git push``` 만 입력해도 된다.

```shell
$ git push [-u] [원격저장소alias] [branch명]

$ git push -u origin main
```

## ```git pull``` 명령어

원격 저장소의 변경사항을 워킹트리에 반영한다. ```git fetch```+```git merge``` 의 명령어가 한번에 실행되는 명령어이다.

```shell
$ git pull
```

## ```git fetch [원격저장소alias] [branch명]``` 명령어

원격 저장소의 branch와 commit 을 로컬 저장소와 동기화 한다. 옵션 생략 시 모든 원격 저장소의 모든 branch 를 가져온다.

```shell
$ git fetch [원격저장소alias] [branch명]
```

## ```git clone [프로젝트의 Github 상 주소]``` 명령어

GitHub에 있는 프로젝트를 내 컴퓨터로 가져온다.

```shell
$ git clone [프로젝트의 Github 상 주소]
```

## ```git merge [branch명]``` 명령어

지정한 branch 의 commit 을 현재 branch 및 워킹트리에 반영한다.

```shell
$ git merge [branch명]
```

##  ```git log``` 명령어

HEAD와 관련된 commit 정보가 자세하게 표시된다.

```shell
$ git log
```

## ```git log --oneline``` 명령어

commit의 hash 정보와 title을 간단하게 표시한다.

```shell
$ git log --oneline
```

##   ```git log --oneline --graph --decorate``` 명령어

HEAD와 관련된 commit 정보를 자세하게 표시한다.

```shell
$ git log --oneline --graph --decorate
```

## ```git log --oneline --graph --all --decorate``` 명령어

모든 branch 정보를 표시한다.

```shell
$ git log --oneline --graph --all --decorate
```

## ```git log -n[숫자]``` 명령어

전체 commit 중에서 전체 n개의 commit만 표시한다.

```shell
$ git log -n[숫자]
```

## ```git log --oneline -n5``` 명령어

현재 branch의 최신 commit 중 5개만 표시한다.

```shell
$ git log --oneline -n5
```

### log 옵션

|   옵션   | 설명                                                         |
| :------: | ------------------------------------------------------------ |
| oneline  | commit 메시지를 한 줄로 요약해서 표시한다. 생략하면 commit 정보를 자세히 표시한다. |
|  graph   | commit 옆에 branch의 흐름을 graph로 보여준다.                |
| decorate | --decorate=short 옵션을 의미한다. branch와 tag 등의 참조를 간결히 표시한다. |
|   all    | all 옵션이 없을 경우 HEAD와 관계없는 옵션은 표시하지 않는다. |

## ```git diff [commit A의 id] [commit B의 id]``` 명령어

두 commit 간의 차이를 비교한다.

```shell
$ git diff [commit A의 id] [commit B의 id]
```

## `git tag [Tag 이름] [commit id]` 명령어

특정 commit에 태그를 붙여서 관리한다.

```shell
$ git tag [Tag 이름] [commit id]
```

## ```git status``` 명령어

워킹 디렉토리에 있는 파일의 상태에 대해서 표시한다.

```shell
$ git status
```

## ```git help [명령어]``` 명령어

git 명령어에 대한 도움말을 조회한다.

```shell
$ git help log
$ git help status
$ git help add
```

## ```git remote add [원격저장소 이름] [원격저장소 주소]``` 명령어

원격저장소를 등록한다. 원격저장소는 여러 개 등록할 수 있지만 같은 별명의 원격저장소는 하나만 가저갈 수 있다. 통산 첫 번째 원격저장소를 origin 으로 지정한다.

```shell
$ git remote add [원격저장소 이름] [원격저장소 주소]
```

## ```git remote -v``` 명령어

원격저장소의 목록을 표시힌다.

```shell
$ git remote -v
```

## `git branch [새 branch 이름]` 명령어

새로운 branch를 생성한다.

```shell
$ git branch [새 branch 이름]
```

## `git checkout -b [새 branch 이름]` 명령어

새로운 branch를 생성하고 그 branch로 바로 이동한다.

```shell
$ git checkout -b [새 branch 이름]
```

## `git branch -d [기존 branch 이름]` 명령어

branch를 삭제한다.

```shell
$ git branch -d [기존 branch 이름]
```

## `git checkout [기존 branch 이름]` 명령어

지정한 branch로 이동한다.

```shell
$ git checkout [기존 branch 이름]
```

## ```git switch [기존 branch 이름]``` 명령어

지정한 branch로 이동한다. `checkout` 에서 branch를 변경하는 부분만 담당한다.

```shell
$ git switch [기존 branch 이름]
```

## ```git switch -c [새 branch 이름]``` 명령어

새로운 branch를 생성하고 그 branch로 바로 이동한다. `checkout -b` 와 동일한 명령어이다.

```shell
$ git switch -c [새 branch 이름]
```

## `git restore [파일명]` 명령어

Working tree 의 파일을 복원한다. 
파일의 수정 내용(README.md 파일을 수정했다고 했을 때)을 복원하려면 `git checkout -- README.md`처럼 사용했는데 이젠 다음과 같이 사용할 수 있다.

```shell
$ git resotre README.md
```

## `git restore --staged [파일명]` 명령어

staging 여역의 파일을 복원한다.
`git add` 명령어을 통해 staging 영역에 있는 파일을 빼려면 `git reset HEAD README.md`처럼 사용하였는데, 다음과 같이 사용 가능하다.

```shell
$ git restore --staged README.md
```

## `git merge [기존 branch 이름]` 명령어

현재 branch에 다른 branch를 머지한다.

```shell
$ git merge [기존 branch 이름]
```

## `git merge --abort` 명령어

머지를 하다가 conflict가 발생했을 때, 일단은 머지 작업을 취소하고 이전 상태로 돌아간다.

```shell
$ git merge --abort
```

## `git blame [파일명]` 명령어

특정 파일의 내용 한줄한줄이 어떤 커밋에 의해 생긴 것인지 출력 

```shell
$ git blame [파일명]
```

## `git revert` 명령어

특정 커밋에서 이루어진 작업을 되돌리는(취소하는) 커밋을 새로 생성한다. 즉 새로운 커밋이 생성되고 파일들의 내용은 이전 커밋이다.

```shell
$ git revert
```

## `git reflog` 명령어

HEAD가 그동안 가리켜왔던 커밋들의 기록을 출력한다. reset 명령어 실행 후 이전 commit id 가 출력되지 않을 때 찾는데 유용한다.

```shell
$ git reflog
```

## `git rebase [branch 이름]` 명령어

A, B branch가 있는 상태에서 지금 HEAD가 A branch를 가리킬 때, git rebase B를 실행하면 A, B branch가 분기하는 시작점이 된 공통 커밋 이후로부터 존재하는 A branch 상의 커밋들이 그대로 B branch의 최신 커밋 이후로 이어붙여진다. (git merge와 같은 효과를 가지지만 커밋 히스토리가 한 줄로 깔끔하게 된다는 차이점이 있다)

```shell
$ git rebase [branch 이름]
```

## `git stash` 명령어

현재 작업 내용을 스택 영역에 저장 한다.

```shell
$ git stash
```

## `git stash apply [commit id]` 명령어

스택 영역에 저장된 가장 최근의(혹은 특정) 작업 내용을 working directory에 적용한다.

```shell
$ git stash apply [commit id]
```

## `git stash drop [commit id]` 명령어 

스택 영역에 저장된 가장 최근의(혹은 특정) 작업 내용을 스택에서 삭제한다.

```shell
$ git stash drop [commit id]
```

## `git stash clear` 명령어

스택 영역에 저장된 모든 작업 내용을 스택에서 삭제한다.

```shell
$ git stash clear
```

## `git stash pop [commit id]` 명령어

스택 영역에 저장된 가장 최근의(혹은 특정) 작업 내용을 working directory에 적용하면서 스택에서 삭제한다.

```shell
$ git stash pop [commit id]
```

## `git cherry-pick [commit id]` 명령어

특정 커밋의 내용을 현재 커밋에 반영한다. branch에 관계없이 사용 가능하다.

```shell
$ git cherry-pick [commit id]
```



# 별첨

## git 과 SVN

git 에서의 commit 은 Delta (차이점) 이 아니라 Snapshot (스냅사진) 으로 처리한다. 즉, 바뀐 내용에 대해서만 저장하는 것이 아니라 수정된 파일을 저장한다. 이에 비해 SVN은 Delta 에 대해서만 저장한다.

## commit 에 포함된 정보

- commit한 사용자 ID
- commit한 날짜와 시간
- commit 메시지

## commit 메시지 작성 할 때 고려 사항

1. 제목과 본문 사이에 빈 줄을 넣어 분리한다.
2. 제목은 50자 이내로 한다.
3. 제목에는 마침표(full stop)을 넣지 않는다.
4. 제목을 영어로 작성 할 때 첫 글자는 대문자로 한다.
5. 제목을 영어로 작성 할 때 동사원형(현재형) 으로 한다.
6. 본문을 72자 단위로 줄바꿈한다.
7. 어떻게(How) 보다 무엇(What)과 왜(Why)를 작성한다.
   1. 왜 Commit 을 했는지 ?
   2. 왜 문제가 발생했는지 ?
   3. 적용한 해결책이 어떤 효과를 가지는지


무엇보다 다른 사람들이 자신의 코드를 바로 이해 할 수 있다고 가정하지 말고 최대한 친절하게 작성한다.

## commit 할 때 알아야 할 가이드 라인

1. 하나의 commit에는 하나의 수정사항, 하나의 이슈(issue)를 해결한 내용만 남기도록 한다. 다양하게 수정을 하고나서 하나의 commit으로 남기는 것은 좋지 않다. 하나의 commit이 하나의 사실만을 갖고 있어야 나중에 이해하기 쉽다.
2.  현재 프로젝트 디렉토리의 상태가 그 내부의 전체 코드를 실행했을 때 에러가 발생하지 않는 상태인 경우에만 commit을 하도록 한다. 나중에 동료 개발자가 특정 commit의 코드로 실행했을 때 에러가 발생한다면 혼란을 줄 수 있다.

## Merge 의 종류

- Fast-forward Merge
  - 한 줄로 되어 있는 branch의 이동
- 3-way Merge
  - base때의 내용과 비교했을 때 달라진 부분이 있는 것이 우선
  - 두 branch에서 둘다 변화가 일어났을 때는 Conflict를 발생시켜서 사용자가 스스로 선택

## git push와 git pull 의 작업 단위

- 작업 단위는 브랜치
- 예를 들어, master 브랜치에서 git push를 하면 master 브랜치의 내용만 리모트 레포지토리의 master 브랜치로 전송되지, premium 브랜치의 내용이 전송되는 것은 아니다.
- git push에 --all이라는 옵션을 주면 모든 브랜치의 내용을 전송 가능

# 읽어보면 git에 대해 이해하기 좋은 사이트

[ProGit](https://git-scm.com/book/ko/v2)

[Gerrit을 이용한 코드 리뷰 시스템 - Gerrit과 Git](https://d2.naver.com/helloworld/1859580)

## 참고자료

[log 명령어의 Pretty 옵션](https://git-scm.com/docs/pretty-formats)

[commit 가이드 라인](https://git-scm.com/docs/git-commit#_discussion)
