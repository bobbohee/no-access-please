---
layout: post
category: python
---

# 문제

이번에 new 맥북에 다시 개발환경을 세팅했다. 
pyenv로 파이썬 3.8.5에 가상환경을 생성하고, 적용하고, 파이썬 버전을 확인해보니 이상하게도 `2.X` 버전 대가 나왔다. (???)

```bash
$ pyenv virtualenv 3.8.5 venv
$ pyenv local venv 
$ python -V
2.7.10
```

<br>

이 상황... 어딘가 익숙하다...

저번에 수아도 똑같은 상황을 겪었는데 `~/.zshrc` 파일에 작성한 pyenv 설정이 잘못되어서 그런 것이었다.
하지만 나는 이전 맥북에서 사용하던 `~/.zshrc` 파일을 그대로 가져와 사용했는데...🤔?

# 해결

아래 참고한 링크에서 설정을 보니 나랑 달랐다. 나한테 없는 설정을 추가해주니 정상적으로 동작했다. (???)

빅서를 사용하다 카탈리나로 다운그레이드를 했는데 카탈리나에서는 설정이 다른가...? 왜인지는 모르겠다... 🤔🤔🤔

<br>

**변경 전**

```bash
export PATH="$HOME/.pyenv/bin:$PATH"
eval "$(pyenv init -)"
eval "$(pyenv virtualenv-init -)"
export PYENV_VIRTUALENV_DISABLE_PROMPT=1
```

**변경 후**

```bash
export PYENV_ROOT="$HOME/.pyenv"
export PATH="$PYENV_ROOT/bin:$PATH"
eval "$(pyenv init --path)"
eval "$(pyenv init -)"
eval "$(pyenv virtualenv-init -)"
export PYENV_VIRTUALENV_DISABLE_PROMPT=1
```

# 참고

[https://info-lab.tistory.com/375](https://info-lab.tistory.com/375){:target="_blank"}