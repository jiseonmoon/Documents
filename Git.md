# git 사용법

## 1. Git의 기본

### 1.1. Git 설치

1. https://git-scm.com/downloads에서 Git for Windows 설치

### 1.2. 초기 설정

1. 설치한 Git에 본인의 사용자명과 메일 주소를 등록

   ```
   git config --global user.name "사용자명"
   git config --global user.email "메일 주소"
   ```

### 1.3. 저장소 설정

- **기존 디렉토리를 Git 저장소로 만들기**

  1. 프로젝트의 디렉토리로 이동한다.

     ```
     cd 프로젝트의 디렉토리
     ```

  2. 깃을 시작

     ```
     git init
     ```

  3. 원격 저장소와 등록

     ```
     git remote add origin 원격 저장소 경로
     ```

- **기존 저장소를 Clone하기**

  1. 폴더를 하나 만들고, 그 안에서 아래 명령을 실행

     ```
     git clone 원격 저장소 경로
     ```



## 2. Git의 기초 명령어

### 2-1. 작업의 흐름 이해하기

**로컬 저장소의 구성**

- 실제 파일들로 이루어져있는 Working directory(작업 디렉토리)
- 준비 영역(staging area)의 역할을 하는 Index(인덱스)
- 최종 확정본을 나타내는 HEAD

![로컬 저장소는 이렇게 생겼어요.](https://rogerdudler.github.io/git-guide/img/trees.png)

### 2-2. 추가와 확정(commit)

1. 변경된 파일을 Index에 추가

   ```
   git add 파일 이름
   ```

2. 변경된 파일을 HEAD에 반영

   ```
   git commit -m "이번 확정본에 대한 설명"
   ```

### 2-3. 변경 내용 발행(push)

1. 로컬 저장소의 HEAD 안에 머물고 있는 변경 내용을 원격 서버로 발행

   ```
   git push origin master
   ```

### 2-4. 끌어오기(pull)

1. 원격 저장소의 데이터를 로컬 저장소에 가져와 병합

   ```
   git pull
   ```



## 3. branch(가지)

### 3-1. 브랜치 이해하기

- 브랜치 : 독립적으로 어떤 작업을 진행하기 위한 개념
- 필요에 의해 만들어지는 각각의 브랜치는 다른 브랜치의 영향을 받지 않기 때문에, 여러 작업을 동시에 진행할 수 있음

1. 저장소를 새로 만들면 기본으로 master 브랜치가 생성
2. 다른 브랜치를 이용해서 개발을 진행하고, 나중에 개발이 완료되면 master 브랜치로 돌아와 병합

![가지치기 예제를 보여드리죠.](https://rogerdudler.github.io/git-guide/img/branches.png)

### 3-2. 브랜치 생성

```
git branch 브랜치명
```

### 3-3. 브랜치 전환

```
git checkout 브랜치명
```

### 3-4. 브랜치 병합

현재 브랜치에 다른 브랜치에 있는 변경 내용을 병합

```
git merge 브랜치명
```

### 3-5. 브랜치 삭제

```
git branch -d 브랜치명
```

### 3-6. 브랜치 비교

```
git diff 브랜치명1 브랜치명2
```

### 3-7. 가져오기

원격 저장소의 데이터를 로컬에 가져오기만 하기

```
git fetch
```

> pull = fetch + merge



## 4. tag(꼬리표)

### 4-1. 태그 이해하기

- 태그 : 커밋을 참조하기 쉽도록 알기 쉬운 이름을 붙이는 것
- 한 번 붙인 태그는 브랜치처럼 위치가 이동하지 않고 고정됨

### 4-2. 태그 추가하기

```
git tag 태그명
```

### 4-3. 주석이 달린 태그를 추가하기

```
git tag -am "주석" 태그명
```

### 4-4. 태그 삭제하기

```
git tag -d 태그명
```