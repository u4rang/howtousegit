# How to use git by CLI
This repository is to explain how to use git by cli.

----

# 용어 정리

|                용어                 | 설명                                                         |
| :---------------------------------: | :----------------------------------------------------------- |
|    워킹트리<br />(Working Tree)     | - 일반적인 작업이 일어나는 곳<br />- 사용자가 파일과 하위 디렉토리를 만들고 작업 결과물을 저장하는 위치 |
| 로컬저장소<br />(Local Repository)  | - ```$git init``` 명령어으로 생성되는 ```.git``` 디렉토리<br />- git 디렉토리, commit 으로 생성되는 정보 저장 |
| 원격저장소<br />(Remote Repository) | - 로컬 저장소를 업로드하는 곳<br />- GitHub 의 저장소        |
|             Git 저장소              | - git 명령어로 관리하는 디렉토리 전체<br />- 좁은 의미로는 로컬저장소를 의미, 넓은 의미로는 워킹트리 |

# 옵션 설정

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

# git 명령어

## ```git add``` 명령어

파일을 Stage 에 추가한다.

```shell
$ git add <파일명1> <파일명2> ...
```

## ```git add --all``` 명령어

```git add``` 명령어와 동일하게 파일을 Stage 에 추가한다. 차이점은 ```git add --all``` 명령어는 변경된 tracked 상태의 파일과 untracked 상태의 파일을 Stage 에 추가하기 때문에 변경 내역을 commit 전 branch를 이동할 때 유용하다.

```shell
$ git add --all
```

## ```git commit``` 명령어

Stage 에 있는 파일을 commit 한다.

```shell
$ git commit
```

## ```git commit -a``` 명령어

```git add``` 명령어를 생략하고 바로 commit 하는 경우 사용한다. 변경된 파일과 삭제된 파일은 stage 단계를 지나 commit 된다. 단, untracked 파일은 commit 되지 않는다.

```shell
$ git commit -a
$ git commit --all
```

## ```git push [-u] [원격저장소alias] [branch 명]``` 명령어

현재 브랜치에서 새로 생성한 commit 을 원격저장소에 업로드한다. -u 옵션으로 branch의 upstream을 등록할 수 있다. 1회 등록 후 ```git push``` 만 입력해도 된다.

```shell
$ git push [-u] [원격저장소alias] [branch명]
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

## ```git log -n<숫자>``` 명령어

전체 commit 중에서 전체 n개의 commit만 표시한다.

```shell
$ git log -n<숫자>
```

## ```git log --oneline -n5``` 명령어

현재 브랜치의 최신 commit 중 5개만 표시한다.

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

## ```git status``` 명령어

워킹 디렉토리에 있는 파일의 상태에 대해서 표시한다.

```shell
$ git status
```

## ```git reset <파일명>``` 명령어

스테이지 영역에 있는 파일을 스테이지 영역에서 제외한다.(언스테이징) 워킹트리의 내용은 변경되지 않는다. 옵션을 생략할 경우 스테이지의 모든 변경사항을 초기화한다.

```shell
$ git reset <파일명>
```

### reset 옵션

| 옵션  | 설명 |
| :---: | ---- |
| soft  |      |
| mixed |      |
| hard  |      |

## ```git help <명령어>``` 명령어

git 명령어에 대한 도움말을 조회한다.

```shell
$ git help log
$ git help status
$ git help add
```

## ```git remote add <원격저장소 이름> <원격저장소 주소>``` 명령어

원격저장소를 등록한다. 원격저장소는 여러 개 등록할 수 있지만 같은 별명의 원격저장소는 하나만 가저갈 수 있다. 통산 첫 번째 원격저장소를 origin 으로 지정한다.

```shell
$ git remote add <원격저장소 이름> <원격저장소 주소>
```

## ```git remote -v``` 명령어

원격저장소의 목록을 표시힌다.

```shell
$ git remote -v
```



# 별첨

## git 과 SVN

git 에서의 commit 은 Delta (차이점) 이 아니라 Snapshot (스냅사진) 으로 처리한다. 즉, 바뀐 내용에 대해서만 저장하는 것이 아니라 수정된 파일을 저장한다. 이에 비해 SVN은 Delta 에 대해서만 저장한다.

## commit 메시지 작성 할 때 고려 사항

1. 제목과 본문 사이에 빈 줄을 넣어 분리한다.
2. 제목은 50자 이내로 한다.
3. 제목에는 마침표(full stop)을 넣지 않는다.
4. 제목을 영어로 작성 할 때 첫 글자는 대문자로 한다.
5. 제목을 영어로 작성 할 때 동사원형(현재형) 으로 한다.
6. 본문을 72자 단위로 줄바꿈한다.
7. 어떻게(How) 보다 무엇(What)과 왜(Why)를 작성한다.

# 읽어보면 git에 대해 이해하기 좋은 사이트

[ProGit](https://git-scm.com/book/ko/v2)

[Gerrit을 이용한 코드 리뷰 시스템 - Gerrit과 Git](https://d2.naver.com/helloworld/1859580)

