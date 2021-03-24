---
layout: post
category: git 
---

# 해결

## 특정 삭제

아래 명령어를 통해 `stash` 목록을 확인한다.

```bash
git stash list
```

stash 목록 중 삭제하고 싶은 stash의 `index`를 적어주면 된다.

```bash
git stash drop stash@{index}
```

## 전체 삭제 

전체 stash를 삭제하고 싶은 경우 `clear`를 사용한다.

```bash
git stash clear
```

# 참고

[https://stackoverflow.com/questions/11369375/how-can-i-delete-all-of-my-git-stashes-at-once/11369406](https://stackoverflow.com/questions/11369375/how-can-i-delete-all-of-my-git-stashes-at-once/11369406){:target="_blank"}