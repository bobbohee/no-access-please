---
layout: post
category: terminal
---

# 문제

터미널을 이용하다 현재 경로를 파인더로 열 수 있지 않을까? 하고 생각해본 적이 없었다.

그러다 문득 명령어가 있지 않을까 하고 검색해보니 실제로 명령어가 있었다. (유레카! 🙊)

# 해결

`open` 명령어를 사용하고, `.`은 현재 경로를 의미해 현재 경로를 파인더로 열어준다.

현재 경로가 아닌 다른 경로를 파인더로 열고 싶다면 '.' 대신 열고 싶은 경로를 입력하면 된다.

```bash
$ open .
```

<br>

`open` 명령어를 사용해 파일도 열 수 있다.

```bash
$ open config/.odoorc
```

# 참고

[https://alvinalexander.com/blog/post/mac-os-x/open-finder-window-in-current-directory-off-terminal-window/](https://alvinalexander.com/blog/post/mac-os-x/open-finder-window-in-current-directory-off-terminal-window/){:target="_blank"}