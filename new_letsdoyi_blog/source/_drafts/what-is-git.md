---
title: "Git이란 무엇일까"
date: 2019-05-02 10:16:42
tags:
  - Git
categories:
  - Tool
  - Git
---

_내용은 계속 수정 및 업데이트 예정_
_markdown도 적응중_

## Git이란 무엇일까 \_ 이력 저장소

Git is a **distributed version-control system** for **tracking changes in source code** during software development. It is designed for coordinating work among programmers, but it can be used to track changes in any set of files. (Wikipedia)

깃이란, 한마디로 **이력 저장소** 이다. 개발자들이 협업을 효율적으로 할 수 있도록 변경사항들을 추적할 수 있는 시스템이다. 변경사항은 소스코드 뿐아니라 파일의 변화도 포함한다.

<!-- more -->

## Git의 컨셉 \_ 가지

git은 master라는 큰 중심 줄기가 있고, 여러 개의 Branch들을 치는 **나무 이미지**를 떠올리면 된다. 여기서 Branch는 격리된 개별 원격 저장소 보면 된다.

개발자1은 작업하여 branch1에 자신의 작업물을 저장하고, 개발자2는 작업하여 branch2에 자신의 작업물을 저장하고, 개발자3는 작업하여 branch3에 자신의 작업물을 저장하고, 개발자4는 작업하여 branch4에 자신의 작업물을 저장하고, 개발자5는 작업하여 branch5에 자신의 작업물을 저장하고...이렇게 각자 개별 작업이 끝나면 각 Branch 들을 큰 중심줄기와 합한다 (Merge).

정리하면,
Git은 큰 중심 저장소(master)에 다른 여러사람들이 작업할 개별 작은 저장소(branch)를 만들고, 개별 작업이 끝날때 마다 큰 중심저장소에 병합 Merge 하여 협업을 효율적으로 도울 수 있다.

1. 개별 원격 저장소 생성 (master가 없을 경우 자동생성된다)
2. 작업 후 결과물 저장
3. 개별 원격 저장소의 작업물들을 master에 병합

## Git 만들기 \_ 새롭게 혹은 복제하여

git을 만들기 위해선 git은 _새롭게_ 만들거나, _기존의 저장소를 복제_ 하여 만들 수 있다. git을 생성하면 **로컬 저장소**와 **원격 저장소**가 생성된다.

다음은 git 생성 2가지 Terminal commands 이다.

```shell
$ git init //현재 속해있는 폴더안에 새로운 git저장소가 만들어 진다.
```

```shell
$ git clone <위치> //저장소를 복제하여 받아온다. <위치> 부분에는 로컬경로를 넣거나, 원격서버의 저장소경로를 넣을 수 있다 (예 https://gitlab.com/~)
```

## Git이 제공하는 로컬 저장소 이해하기 \_ 중간에 준비영역을 거친다(Index)

개발자1이 작업하여 **branch1(개별 원격 저장소)**에 자신의 작업물을 저장할 때, **깃이 제공하는 로컬 저장소 (Local Repository)**에서 **개별 원격 저장소**로 작업물을 옮기는 과정을 거친다.

**''깃이 제공하는 로컬 저장소(Local Repository)''**
개발자 1이 작업하던(in workingspace) 작업물은 Index(준비영역)을 거처 깃이 제공하는 로컬 저장소에 저장된다.

**Workspace** — **Index** — **Local Repository**

다음은 로컬 저장소까지 파일들을 추가, 확정하기 위한 Terminal commands이다.

#### 1. Workspace to Index

```shell
$ git add <OPTION>
```

위의 명령어를 사용하면, Index에 add 할 수 있다

#### 2. Index to Local Repository

```shell
$ git commit -m <DESCRIPTION>
```

위의 명령어를 사용하면, 확정된 파일을 로컬 저장소에 commit 시킬 수 있다

#### 3. Local Repository to Remote Repository (Branch)

```shell
$ git push origin <BRANCH NAME>
```

위의 명령어를 사용하면, 로컬 저장소에 있는 파일들을 개별 원격저장소로 push 시킬 수 있다

`git add <option>`

1. `git add -A` 아래경우 모두 포함 할 때
2. `git add .` 새 파일과 수정된 파일이 있을때
3. `git add -U` 수정된 파일과 삭제된 파일이 있을 때 (새로운 파일은 없을때)

`git commit -m <DESCRIPTION>`
`<DESCRIPTION>`이 부분에는 설명을 적을 수 있다. (코멘트 같은 느낌)

---
