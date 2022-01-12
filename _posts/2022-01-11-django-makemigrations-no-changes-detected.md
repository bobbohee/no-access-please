---
layout: post
category: django
---

# 문제

`패스트캠퍼스 > 한 번에 끝내는 파이썬 웹 개발 초격차 패키지 Online > Part7. Django 기초 > Ch1. Django와 친해지기 > 05. Database Modeling (2)` 강의에서 `PayPlan` 테이블을 생성하고, `makemigrations`을 진행하니 변경 사항이 없다는 메세지가 나왔다.

```python
from django.db import models

# Create your models here.

class PayPlan(models.Model):
    name = models.CharField(max_length=20) # max_length를 지정하지 않으면 오류 발생
    price = models.IntegerField()
    updated_at = models.DateField(auto_now=True)
    create_at = models.DateTimeField(auto_now_add=True)
```

```bash
$ python manage.py makemigrations
No changes detected
```

# 해결

`settings.py` 파일에 `INSTALLED_APPS`에 App을 추가해줘야한다.

```python
# shrinkers/shrinkers/settings.py
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'shortener.apps.ShortenerConfig', # 추가 (shrinkers/shortener/apps.py 확인)
]
```

<br>

App을 추가하고 다시 `makemigrations`을 진행하니, `PayPlan` 모델이 생성되었다!

```bash
$ python manage.py makemigrations
Migrations for 'shortener':
  shortener/migrations/0001_initial.py
    - Create model PayPlan

$ python manage.py migrate
Operations to perform:
  Apply all migrations: admin, auth, contenttypes, sessions, shortener
Running migrations:
  Applying shortener.0001_initial... OK
```

# 참고

[https://wonwooddo.tistory.com/75](https://wonwooddo.tistory.com/75){:target="_blank"}