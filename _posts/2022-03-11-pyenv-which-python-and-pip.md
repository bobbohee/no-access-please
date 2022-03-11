---
layout: post
category: python
---

# 문제

Ubuntu, Bitnami에서 Odoo, Django 등 파이썬 서버를 가상 환경으로 실행시켜야 하는 경우, 서비스(service) 파일에서 가상 환경 위치를 지정해주어야 한다.

# 해결

### python

```
$ pyenv which python
/Users/bobbohee/.pyenv/versions/hw_esg_3.9/bin/python
```

### pip

`Location`을 보면 패키지가 설치된 경로를 알 수 있다.

```
$ pip show django
Name: Django
Version: 3.2
Summary: A high-level Python Web framework that encourages rapid development and clean, pragmatic design.
Home-page: https://www.djangoproject.com/
Author: Django Software Foundation
Author-email: foundation@djangoproject.com
License: BSD-3-Clause
Location: /Users/bobbohee/.pyenv/versions/3.9.2/envs/hw_esg_3.9/lib/python3.9/site-packages
Requires: asgiref, pytz, sqlparse
Required-by: django-cors-headers, django-excel, django-filter, django-import-export, django-seed, djangorestframework, djangorestframework-simplejwt, drf-yasg
```

# 참고

[https://velog.io/@markyang92/python-pyenv#-pyenv-which-python](https://velog.io/@markyang92/python-pyenv#-pyenv-which-python)