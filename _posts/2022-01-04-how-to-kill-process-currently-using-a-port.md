---
layout: post
category: odoo
---

# 문제

개인 블로그 (공개), 개인 블로그 (비공개), 회사 블로그까지 3개 블로그에서 글을 작성하다보니, 제대로 서버를 종료하지 않아서`Address already in use` 에러가 발생했다.

```bash
/Users/bobbohee/.rbenv/versions/2.7.4/lib/ruby/2.7.0/socket.rb:201:in 'bind': Address already in use - bind(2) for 127.0.0.1:4000 (Errno::EADDRINUSE)
```

# 해결

`lsof -i:[포트]` 명령어로 현재 실행 중인 프로세스를 확인한다.

```bash
$ lsof -i:4000
COMMAND   PID     USER   FD   TYPE             DEVICE SIZE/OFF NODE NAME
ruby    53869 bobbohee    9u  IPv4 0xdaa280f9bc8a29dd      0t0  TCP localhost:terabase (LISTEN)
```

<br>

프로세스를 종료하기 위해서는 `PID` 값이 필요한데, `-t` 옵션을 추가하면 `PID` 값을 알 수 있다.

```bash
$ lsof -t -i:4000
53869
```

<br>

`kill -9 [PID]` 명령어로 현재 실행 중인 프로세스를 종료하면 된다.

```bash
$ kill -9 $(lsof -t -i:4000)
$ kill -9 53869
```

# 참고

[https://stackoverflow.com/questions/11583562/how-to-kill-a-process-running-on-particular-port-in-linux](https://stackoverflow.com/questions/11583562/how-to-kill-a-process-running-on-particular-port-in-linux){:target="_blank"}