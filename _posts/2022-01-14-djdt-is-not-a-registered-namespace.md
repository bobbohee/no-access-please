---
layout: post
category: django
---

# 문제

`패스트캠퍼스 > 한 번에 끝내는 파이썬 웹 개발 초격차 패키지 Online > Part7. Django 기초 > Ch2. Django 다뤄보기 > 01. Django 데이터베이스 관리 - ORM` 강의를 따라
Debug Toolbar 설정을 진행하고, 서버를 실행시키니 `KeyError: 'djdt'` 오류가 발생했다.

```bash
System check identified no issues (0 silenced).
January 14, 2022 - 01:26:47
Django version 3.2, using settings 'shrinkers.settings'
Starting development server at http://127.0.0.1:8000/
Quit the server with CONTROL-C.
Internal Server Error: /
Traceback (most recent call last):
  File "/Users/bobbohee/.pyenv/versions/dev_online_pyweb_part7_shrinkers/lib/python3.8/site-packages/django/urls/base.py", line 71, in reverse
    extra, resolver = resolver.namespace_dict[ns]
KeyError: 'djdt'
```

# 해결

검색해보니 강의에서는 따로 설명이 없었지만 추가로 `urlpatterns`을 등록해주어야 했다.

[공식 문서](https://django-debug-toolbar.readthedocs.io/en/latest/installation.html#add-the-urls){:target="_blank"}를 참고해서 `urlpatterns`을 등록하고 실행하니, 또 다른 오류가 발생했다.

```python
import debug_toolbar
from django.urls import path, include

urlpatterns = [
    path('__debug__/', include('debug_toolbar.urls')),
]
```

```bash
ModuleNotFoundError: No module named 'debug_toolbar.urls'
```

<br>

`'debug_toolbar.urls'`를 감싼 따옴표를 제거하니 정상적으로 Debug Toolbar가 실행되었다.
공식 문서가 잘못 작성된 것 같다. 😅

```python
urlpatterns = [
    path('__debug__/', include(debug_toolbar.urls)),
]
```

# 참고

[https://stackoverflow.com/questions/51985367/after-adding-django-debug-to-app-getting-djdt-is-not-a-registered-namespace](https://stackoverflow.com/questions/51985367/after-adding-django-debug-to-app-getting-djdt-is-not-a-registered-namespace){:target="_blank"}
