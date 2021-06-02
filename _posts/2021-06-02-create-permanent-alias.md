---
layout: post
category: etc  
---

# 문제

블로그 포스트 작성 시, 작성한 포스트를 로컬에서 먼저 확인하기 위해 실행하는 명령어가 입력하기 번거롭다는 생각이 들어 `alias`로 등록해놓았었다.

```bash
$ alias bejs="bundle exec jekyll serve"
```

<br>

등록한 alias가 정상 동작하는 것을 확인하고, 다음날 터미널에 `bejs`를 입력했는데 `bejs`를 찾을 수 없다는 메세지가 나타났다.

```bash
$ bejs
zsh: command not found: bejs 
```

# 원인

위 방식으로 등록한 alias는 터미널을 종료하거나, 재부팅하게 되면 설정값들이 초기화되서 사라진다고 한다.

# 해결

alias를 영구적으로 등록해 사용하기 위해서는 `~/.zsh` 파일에 등록해주어야 한다.

```text
alias bejs='bundle exec jekyll serve'
```

# 참고

[https://movenpick.tistory.com/26](https://movenpick.tistory.com/26){:target="_blank"}