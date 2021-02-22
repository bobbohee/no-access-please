---
layout: post
category: odoo
---

# 문제

`ubuntu 18.04`에 오두 서버를 올리면 항상 1~2일 뒤, `ModuleNotFoundError`가 나면서 서비스가 종료되었다.

![Odoo ModuleNotFoundError](/no-access-please/assets/image/2021-02-21-odoo-server-module-not-found-error/1.png)

# 원인

오두 서버별로 `ModuleNotFoundError`가 났던 라이브러리가 달랐는데, 해당 오류가 났던 라이브러리가 전역 설치가 필요한 라이브러리들이었다.

라이브러리 설치 시, `virtualenv`를 사용해 프로젝트 내에 설치했기 때문에 발생한 오류들이었다.

# 해결

`virtualenv` 환경에 접속하지 않고, 필요한 라이브러리들을 전역 설치해주면 된다.

```bash
pip -r requirements.txt
```