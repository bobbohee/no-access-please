---
layout: post
category: django
---

# 문제

`패스트캠퍼스 > 한 번에 끝내는 파이썬 웹 개발 초격차 패키지 Online > Part7. Django 기초 > Ch1. Django와 친해지기 > 06. Django URLs and Views and Models (1)` 강의 진행 중
username으로 User를 검색하는 ORM을 작성했다. 테스트를 해보려면 User 테이블에 레코드가 있어야 하는데, 나는 저번에 DB를 날려서 가입된 유저가 없었다.

그래서 새로 관리자(superuser)를 만들기 위해 명령어를 입력했더니 오류가 발생했다.

```bash
$ python manage.py createsuperuser
Username: bobbohee
Email address: bobbohee.at@gmail.com
Password:
Password (again):

Traceback (most recent call last):
  File "/Users/bobbohee/.pyenv/versions/dev_online_pyweb_part7_shrinkers/lib/python3.8/site-packages/django/db/backends/utils.py", line 84, in _execute
    return self.cursor.execute(sql, params)
  File "/Users/bobbohee/.pyenv/versions/dev_online_pyweb_part7_shrinkers/lib/python3.8/site-packages/django/db/backends/sqlite3/base.py", line 423, in execute
    return Database.Cursor.execute(self, query, params)
sqlite3.IntegrityError: NOT NULL constraint failed: shortener_users.pay_plan_id
```

# 해결

User 테이블에 ForeignKey로 연결된 pay_plan_id가 NOT NULL 제약 조건을 위배해 발생한 오류이다.
만약 NULL 값을 허용하고 싶다면 `null=True`로 설정하면 된다. 기본값은 `False`이기 때문에 자동으로 NOT NULL 제약 조건을 가지게 된다.

```python
from django.db import models
from django.contrib.auth.models import AbstractUser

class Users(AbstractUser):
	pay_plan = models.ForeignKey(PayPlan, on_delete=models.DO_NOTHING, null=True)
```

# 참고

[https://docs.djangoproject.com/ko/3.2/ref/models/fields/#null](https://docs.djangoproject.com/ko/3.2/ref/models/fields/#null){:target="_blank"}
