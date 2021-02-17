---
layout: post
category: git
---

# 해결

## 브랜치 확인

로컬, 원격 브랜치 모두 확인할 수 있다.

```bash
git branch -a
```

### 브랜치 업데이트

원격 브랜치를 확인했을 때, 브랜치가 보이지 않다면 원격 브랜치를 업데이트 한다.

```bash
git remote update
```

## 원격 브랜치 가져오기

### 같은 이름으로 

원격 브랜치와 같은 이름으로 가져온다면 아래 명령어를 사용한다.

```bash
git checkout -t {원격 브랜치명}
```

### 지정한 이름으로 

원격 브랜치와 다른 이름으로 가져온다면 아래 명령어를 사용한다.

```bash
git checkout -b {지정할 브랜치명} {원격 브랜치명}
```

# 참고 사이트

[https://cjh5414.github.io/get-git-remote-branch](https://cjh5414.github.io/get-git-remote-branch){:target="_blank"}