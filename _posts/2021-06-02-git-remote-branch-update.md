---
layout: post
category: git 
---

# 문제 

pull request를 한 후, merge 되고 삭제한 `develop_purchase_view` 브랜치가 로컬에서 확인해보니 남아있었다.

```bash
$ git branch -a
* develop
  remotes/origin/HEAD -> origin/develop
  remotes/origin/develop
  remotes/origin/develop_purchase_view
  remotes/origin/main
```

<br>

기존에 원격 브랜치 정보를 업데이트 하기 위해 아래 명령어를 사용했었는데, 삭제된 브랜치 정보는 업데이트 되지 않았다.

```bash
$ git remote update
```

# 해결

remote 브랜치에 새로 추가되거나 삭제된 브랜치 정보를 최신으로 업데이트할 때는 아래 명령어를 사용해야한다.

```bash
$ git remote prune origin
Pruning origin
URL: https://github.com/foo/bar.git
 * [pruned] origin/develop_purchase_view
```

<br>

삭제한 `develop_purchase_view` 브랜치가 로컬에서도 삭제됨을 확인할 수 있었다.

```bash
$ git branch -a
* develop
  remotes/origin/HEAD -> origin/develop
  remotes/origin/develop
  remotes/origin/main
```

# 참고

[https://webisfree.com/2016-12-16/git-remote-관리-명령어-한눈에-보기](https://webisfree.com/2016-12-16/git-remote-%EA%B4%80%EB%A6%AC-%EB%AA%85%EB%A0%B9%EC%96%B4-%ED%95%9C%EB%88%88%EC%97%90-%EB%B3%B4%EA%B8%B0){:target="_blank"}