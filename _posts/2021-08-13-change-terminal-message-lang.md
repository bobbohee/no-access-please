---
layout: post
category: terminal
---

# 문제

이번에 new 맥북에 새로 개발환경을 세팅했는데, git 메세지가 한글로 출력되었다. 
그 전에는 영문으로 된 메세지로 보고있었기 때문에 한글이 어색하게 느껴져 얼른 바꾸기로 했다!

![한글/영문 메세지](/no-access-please/assets/image/2021-08-13-change-terminal-message-lang/1.png)

# 해결

현재 사용중인 언어를 확인해보니, `ko_KR`로 나왔다.

```bash
$ echo LANG
ko_KR.UTF-8
```

<br>

영구적으로 적용하기 위해서는 설정 파일에 `en_US`로 적어주어야 한다. 

```bash
$ echo 'export LANG=en_US.UTF-8' >> ~/.zshrc
$ source ~/.zshrc
```

# 참고

[https://zetawiki.com/wiki/리눅스_쉘_메시지_영어로_변경하기](https://zetawiki.com/wiki/%EB%A6%AC%EB%88%85%EC%8A%A4_%EC%89%98_%EB%A9%94%EC%8B%9C%EC%A7%80_%EC%98%81%EC%96%B4%EB%A1%9C_%EB%B3%80%EA%B2%BD%ED%95%98%EA%B8%B0){:target="_blank"}