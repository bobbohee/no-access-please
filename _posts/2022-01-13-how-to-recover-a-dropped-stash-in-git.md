---
layout: post
category: git
---

# 문제

git stash를 삭제하다가 실수로 삭제하면 안되는 stash까지 삭제가 되어버렸다. 😭
되돌릴 수 있는 방법이 있을 것 같아 검색해보니 다행히 되돌릴 수 있었다.

# 해결

삭제한 stash의 hash 값을 알면 복구할 수 있다.



<br>

만약 아직 터미널을 종료하지 않았다면, 쉽게 hash 값을 찾을 수 있다.
`()` 안에 있는 문자열이 hash 값이다.

```bash
$ git stash drop stash@{0}
Dropped stash@{0} (28db0a49d6078db45721595d2424031394364995)
$ git stash drop stash@{1}
Dropped stash@{1} (c118133aeabecdd5539953cb7a189fb120f03d65)
```

만약 터미널을 종료해 hash 값을 알 수 없다면, 아래 명령어를 통해 출력된 hash 목록에서 찾아야 한다...

```bash
$ git fsck --no-reflog | awk '/dangling commit/ {print $3}'
```

<br>

`git show` 명령어를 통해 복구하고자 하는 코드가 맞는지 확인할 수 있다.

```bash
$ git show [<stash>]
```

![git show 확인](/no-access-please/assets/image/2022-01-13-how-to-recover-a-dropped-stash-in-git/1.png)

복구하고자 하는 코드가 맞다면 이제 `git stash apply` 명령어를 통해 되돌리면 복구된다!

```bash
git stash apply [<stash>]
```

# 참고

[https://stackoverflow.com/questions/89332/how-to-recover-a-dropped-stash-in-git](https://stackoverflow.com/questions/89332/how-to-recover-a-dropped-stash-in-git){:target="_blank"}

[https://mrgamza.tistory.com/597](https://mrgamza.tistory.com/597){:target="_blank"}
