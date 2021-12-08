---
layout: post
category: terminal
---

# 문제

iterm2를 종료할 때마다 자꾸 업데이트를 하라고 해서 무의식적으로 업데이트 버튼을 눌렀다가 급하게 취소했다.

brew로 설치해야 삭제할 때도 깔끔하게 삭제할 수 있기 때문에 brew로 iterm2를 설치했는데, brew로 업데이트 하지 않는다면 나중에 삭제할 때 깔끔하게 삭제되지 않을 것 같다는 생각이 들어 brew로 업데이트를 하기로 했다.

# 해결

나는 방법2을 사용해 업데이트를 했지만, 스텍오버플로우에서 가장 많은 추천을 받은 건 방법1이다.


## 방법1

```bash
$ brew install iterm2
```

## 방법2

```bash
$ brew update
$ brew upgrade iterm2
$ brew cleanup iterm2
```

<br>

한 번에 입력하고 싶다면, 아래와 같이 입력하면 된다.

```bash
$ brew update && brew upgrade iterm2 && brew cleanup iterm2
```

# 참고

[https://stackoverflow.com/questions/4523920/how-do-i-update-a-formula-with-homebrew](https://stackoverflow.com/questions/4523920/how-do-i-update-a-formula-with-homebrew){:target="_blank"}