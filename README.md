# [git] tag, commit-amend, revert, reset, rebase 

## 목차 

```
1. git tag
2. git comit-amend
3. git revert
4. git reset
5. git rebase -i
```



## 1. git tag

깃 태그는 커밋을 참조하기 쉽도록 알기 이름을 붙일 수 있게 만들어 주는 기능.

커밋 조회시 커밋 번호나 메세지로 커밋을 찾기 어렵다. 

이때 깃 태그를 사용하면 쉽게 찾을 수 있다. 

보통 현업에서는 릴리즈된 버전에 대한 커밋에 태그를 붙혀 사용한다.

**일반 태그** 와 **주석 태그** 로 나뉜다.



### 일반 태그

태그 이름만 붙은 태그를 말한다

##### `$ git tag <tagname>`

마지막 커밋에 태그가 붙는다



### 주석 태그

이름만 붙는 일반 태그와 달리 

- 이름
- 태그설명
- 서명
- 태그 작성자 이름 / 이메일 / 날짜 정보를 가진다.



### git tag 명령어

#### 태그 조회

##### `$ git tag`

##### sample

```bash
$ git tag
#ann_tag
#ingredients
```

#### 원하는 태그명 조건 검색

##### `$ git tag -l <tag_name>`

##### sample

```bash
$ git tag -l ann*
#ann_tag
```

#### 태그 메세지 및 커밋 확인

##### `$ git show <tag_name>`

##### sample

```bash
$ git show ann_tag
#tag ann_tag
#Tagger: soomti <soom93@gmail.com>
#Date:   Tue Nov 27 16:40:04 2018 +0900

#주석 태그를 알아봅시다

#commit 59aae9af1e986c4943c6e23ee76bf891e612235e (HEAD -> master, tag: ingredients, tag: ann_tag, origin/master)
#Author: soomti <soom93@gmail.com>
#Date:   Tue Nov 27 16:02:27 2018 +0900

#   버터 추가

#diff --git a/f b/f
#new file mode 100644
#index 0000000..e69de29
```

#### 태그 삭제 

##### `$ git tag -d <tag_name>`

```bash
$ git tag -d ann_tag
#Deleted tag 'ann_tag' (was 9f402c7)
```



## 2. git commit --amend

마지막 커밋 메세지를 변경할 수 있는 명령어

##### `$ git commit --amend`



## 3. git revert

과거 상태의 커밋을 없었던 일로 만들 수 있다

##### `$ git revert <commit_number> or <tag_name>`

해당 커밋에서 했던 작업들이 사라진다. 또한 해당 커밋을 지웠다는 커밋이 남겨진다!



## 4. git reset

과거 상태의 커밋을 없었던 일로 만들수있다. 

##### `$ git reset <commit_number> or <tag_name> `

3가지 모드가 존재한다 

1. soft

   특정 커밋으로 돌아간 후 **커밋 이후의 내용들을 스테이징에 올려놓은 상태로 남겨놓는다.** 

2. mixed (default)

   특정 커밋으로 돌아간 후 **커밋 이후의 내용들을 스테이징에 올려놓지 않은 상태로 남겨놓는다. **

3. hard

   특정 커밋으로 돌아간 후 **커밋 이후의 내용들을 지운다.**

   _git revert_ 와 이력이 남는점 빼고 다를게 없다! 



## git revert vs git reset

#### **git revert** 

- #### 특정 커밋은 없었던 일로 만들었다는 커밋을 남긴다.

- 커밋한 상황으로 되돌아 가는게 아닌, 그 커밋의 **상태**를 되돌린다.

  따라서 push 여부에 관계없이 커밋을 되돌릴 수 있다.

#### **git reset**

- #### 특정 커밋으로 돌아갔다는 이력이 남지 않는다. 

- 커밋한 상황으로 되돌아 간다. 즉 그 커밋의 **시간**으로 복구됨. 

  push 를 한 커밋의 경우 그 시간으로 되돌리더라도, 

  원격 저장소의 시간을 되돌릴 수 없기 때문에 push 이후의 커밋은 사용할 수 없다. 


따라서 _push_ 를 한상태더라도, 상태를 바꾸기 때문에 특정 커밋을 없었던 

- git revert 는 특정 커밋을 없었던 일로 만들었다는 이력을 남긴다.
- git reset 은 남기지 않고 완전한 그 시간 상태로 reset 한다 
- Revert는 상태를 되돌린다고 볼 수 있습니다. 스포를 당한 커밋을 revert하고 현재 작성중인 코드만 본다면 reset과 동일한 (hard 옵션 준거만 빼고) 결과를 가집니다. 하지만 이력은 같지 않습니다. 먼저 결과를 먼저 보고 이어가겠습니다. (reset과 동일하게 스포일러를 당한 것을 되돌립니다)



## git rebase -i

과거의 커밋메세지를 관리할 때 사용한다. 여러 커밋을 한번에 수정할 수 있다.

##### `$ git rebase -i HEAD~N`

마지막 커밋(HEAD)부터 N번째까지 커밋을 불러온다. 

#### pick

**pick** 은 커밋을 사용하겠다는 의미이다. 커밋의 순서를 바꿀 수 있다. 

#### reword

**reword** 는 커밋 메시지를 변경하는 명령어이다.

#### squash

**squash** 은 해당 커밋을 이전 커밋과 합치는 명령어이다.