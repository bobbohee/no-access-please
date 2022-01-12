---
layout: post
category: django
---

# 문제

`패스트캠퍼스 > 한 번에 끝내는 파이썬 웹 개발 초격차 패키지 Online > Part7. Django 기초 > Ch1. Django와 친해지기 > 05. Database Modeling (3)` 강의에서 기존 장고 User 테이블에 pay_plan 필드를 추가했다.

```python
# shrinkers/shortener/models.py
from django.db import models
from django.contrib.auth.models import AbstractUser

class Users(AbstractUser):
	pay_plan = models.ForeignKey(PayPlan, on_delete=models.DO_NOTHING)
```

```python
# shrinkers/shrinkers/settings.py
AUTH_USER_MODEL = "shortener.Users"
```

<br>

`migrate`을 진행하니 오류가 발생하면서 필드가 추가되지 않았다.

```bash
# 오류 일부 생략
$ python manage.py migrate
Operations to perform:
  Apply all migrations: admin, auth, contenttypes, sessions, shortener
ValueError: The field admin.LogEntry.user was declared with a lazy reference to 'shortener.users', but app 'shortener' doesn't provide model 'users'.
```

# 해결

이미 User 테이블이 생성된 상태에서는 필드 추가를 하기가 어렵다.

shrinkers/shortener/migrations 폴더에서 `__init__.py` 파일을 제외한 폴더와 파일을 삭제한다.
`db.sqlite3` 파일까지 삭제한 후, 다시 `migrations`과 `migrate` 진행하면 테이블이 정상적으로 생성된다.


# 참고

[https://stackoverflow.com/questions/50324561/valueerror-the-field-admin-logentry-user-was-declared-with-a-lazy-reference](https://stackoverflow.com/questions/50324561/valueerror-the-field-admin-logentry-user-was-declared-with-a-lazy-reference){:target="_blank"}

[https://developer0809.tistory.com/95](https://developer0809.tistory.com/95){:target="_blank"}
