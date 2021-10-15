---
layout: post
category: terminal
---

# 문제

터미널에서 `vi`로 파일을 열었을 때, 코드가 하이라이팅이 되지 않고 그냥 흰 글씨로 나타난다.

나는 `vi`로 코드를 편집할 경우는 거의 없고, 설정 파일을 편집할 때 `vi`를 사용하고는 하는데 온통 흰 글씨로 나오니 알아보기가 힘들었다. 😵

![vim 코드 하이하이팅 적용 전](/no-access-please/assets/image/2021-08-16-vim-use-code-highlighting/1.png)

# 해결

`~/.vimrc` 파일에 `syntax on`을 작성하면 코드 하이라이팅이 적용된다.
탭 사이즈나 줄번호 등 기타 설정도 `~/.vimrc`에 작성하면 된다.

```bash
$ echo "syntax on" >> ~/.vimrc
```

<br>

짜잔! 🙌

![vim 코드 하이하이팅 적용 후](/no-access-please/assets/image/2021-08-16-vim-use-code-highlighting/2.png)
