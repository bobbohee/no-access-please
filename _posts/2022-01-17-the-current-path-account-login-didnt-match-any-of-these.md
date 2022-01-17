---
layout: post
category: django
---

# 문제

`패스트캠퍼스 > 한 번에 끝내는 파이썬 웹 개발 초격차 패키지 Online > Part7. Django 기초 > Ch2. Django 다뤄보기 > 05. Django 게시판 구조`에서
로그인하지 않은 사용자는 접속할 수 없도록 `@login_required`를 설정했다.

```python
# shrinkers/shortener/views.py
from django.contrib.auth.decorators import login_required

@login_required
def list_view(request):
    # code
```

<br>

해당 list_view로 접속해보니, 아래와 같이 오류가 발생했다.

```text
The current path, accounts/login/, didn’t match any of these.
```

# 해결

로그인하지 않은 사용자는 로그인 페이지로 리다이렉트 시키는데, django에 기본 로그인 엔드포인트(`/accounts/login`)와 다른 로그인 엔드포인트(`/login`)를 사용해서 발생한 오류이다.

django에 기본 로그인 엔드포인트와 다른 로그인 엔드포인트를 사용하고 싶다면, `LOGIN_URL`을 지정하면 된다.

```python
# shrinkers/shrinkers/settings.py
LOGIN_URL = '/login'
```

# 참고

[https://stackoverflow.com/questions/52445694/the-current-path-account-login-didnt-match-any-of-these](https://stackoverflow.com/questions/52445694/the-current-path-account-login-didnt-match-any-of-these){:target="_blank"}
