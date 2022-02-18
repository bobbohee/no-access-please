---
layout: post
category: django
---

# 문제

`django-seed`를 사용해 10개의 Fake 데이터를 생성하니, 10개의 레코드에 모두 같은 값이 들어갔다.

```python
def handle(self):
    """ 일일 온실가스 배출량 Fake 데이터 생성 """
    seeder = Seed.seeder()
    seeder.add_entity(models.TCO2, 10, {
        'tco2': seeder.faker.pydecimal(left_digits=3, right_digits=1, positive=True, min_value=200, max_value=300),
        'reference_date': seeder.faker.date_between(start_date='-30d'),
        'created_at': datetime.now(),
        'updated_at': datetime.now(),
    })
    created = seeder.execute()
```

![django-seed를 통해 생성한 데이터 1](/no-access-please/assets/image/2022-02-08-django-seed-fixed-data/1.png)

# 해결

`lambda` 함수를 이용하면 레코드마다 다른 값이 들어간다.

```python
def handle(self):
    """ 일일 온실가스 배출량 Fake 데이터 생성 """
    seeder = Seed.seeder()
    seeder.add_entity(models.TCO2, 10, {
        'tco2': lambda x: seeder.faker.pydecimal(left_digits=3, right_digits=1, positive=True, min_value=200, max_value=300),
        'reference_date': lambda x: seeder.faker.date_between(start_date='-30d'),
        'created_at': datetime.now(),
        'updated_at': datetime.now(),
    })
    created = seeder.execute()
```

![django-seed를 통해 생성한 데이터 2](/no-access-please/assets/image/2022-02-08-django-seed-fixed-data/2.png)

# 참고

[https://github.com/Brobin/django-seed](https://github.com/Brobin/django-seed){:target="_blank"}

[https://fenderist.tistory.com/373](https://fenderist.tistory.com/373){:target="_blank"}
