---
layout: post
category: odoo
---

# 문제

odoo를 실행하기 위해 서버를 시작했더니 `Address already in use` 오류가 발생했다.
8069 포트를 사용하고 있었는데 이미 누가 8069 포트를 사용하고 있다는 내용이다.

간혹 다른 프로세서 포트를 사용하고 있는 경우도 있었지만, 거의 대부분은 프로세서가 비상적으로 종료되어서 발생한다.

```
/Users/bobbohee/.pyenv/versions/odoo-ent14-kr/bin/python "/Users/bobbohee/Library/Application Support/JetBrains/Toolbox/apps/PyCharm-P/ch-0/212.4746.96/PyCharm.app/Contents/plugins/python/helpers/pydev/pydevd.py" --multiproc --qt-support=auto --client 127.0.0.1 --port 55930 --file /Users/bobbohee/Documents/parkbohee/ssk/odoo-ent14-kr/config/data/odoo-bin --config=./config/.odoorc_local --dev=all
Connected to pydev debugger (build 212.4746.96)
Traceback (most recent call last):
  File "/Users/bobbohee/.pyenv/versions/3.8.5/lib/python3.8/threading.py", line 870, in run
    self._target(*self._args, **self._kwargs)
  File "/Users/bobbohee/Documents/parkbohee/ssk/odoo-ent14-kr/odoo/service/server.py", line 441, in http_thread
    self.httpd = ThreadedWSGIServerReloadable(self.interface, self.port, app)
  File "/Users/bobbohee/Documents/parkbohee/ssk/odoo-ent14-kr/odoo/service/server.py", line 149, in __init__
    super(ThreadedWSGIServerReloadable, self).__init__(host, port, app,
  File "/Users/bobbohee/.pyenv/versions/odoo-ent14-kr/lib/python3.8/site-packages/werkzeug/serving.py", line 701, in __init__
    HTTPServer.__init__(self, server_address, handler)
  File "/Users/bobbohee/.pyenv/versions/3.8.5/lib/python3.8/socketserver.py", line 452, in __init__
    self.server_bind()
  File "/Users/bobbohee/Documents/parkbohee/ssk/odoo-ent14-kr/odoo/service/server.py", line 165, in server_bind
    super(ThreadedWSGIServerReloadable, self).server_bind()
  File "/Users/bobbohee/.pyenv/versions/3.8.5/lib/python3.8/http/server.py", line 138, in server_bind
    socketserver.TCPServer.server_bind(self)
  File "/Users/bobbohee/.pyenv/versions/3.8.5/lib/python3.8/socketserver.py", line 466, in server_bind
    self.socket.bind(self.server_address)
OSError: [Errno 48] Address already in use
python-BaseException
```

# 해결

`isof` 명령어로 8069 포트를 사용하고 있는 프로세스를 조회한다.

```bash
> lsof -i :8069
COMMAND     PID     USER   FD   TYPE             DEVICE SIZE/OFF NODE NAME
python3.8 81122 bobbohee   49u  IPv4 0xcb4b55e94b895807      0t0  TCP *:8069 (LISTEN)
```

<br>

`kill -9` 명령어로 프로세스를 강제 종료시킨다. `81122`는 위에서 조회한 프로세스의 `PID`를 의미한다.

```bash
> kill -9 81122
```

# 참고

[https://velog.io/@nomadhash/TIL-에러노트-Node-js-address-already-in-use](https://velog.io/@nomadhash/TIL-%EC%97%90%EB%9F%AC%EB%85%B8%ED%8A%B8-Node-js-address-already-in-use){:target="_blank"}