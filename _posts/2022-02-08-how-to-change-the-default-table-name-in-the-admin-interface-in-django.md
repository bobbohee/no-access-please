---
layout: post
category: django
---

# 문제

장고는 기본적으로 모델명을 따로 지정하지 않으면 클래스명을 따라 클래스명이 `CamelCase`라면, 모델명을 `camel case`로 지정한다.
그래서 그런지 admin 페이지에서 `AHU` 모델과 `TCO2` 모델명이 아래와 같이 나왔다.

![모델명 지정 전](/no-access-please/assets/image/2022-02-08-how-to-change-the-default-table-name-in-the-admin-interface-in-django/1.png)

`Ahus`는 `AHUS`로 `Tc o2s`는 `TCO2`로 변경하고 싶었다.

# 해결

정말 간단하다. `class Meta`에 `verbose_name`을 지정하면 된다.

```python
class AHU(models.Model):
    class Meta:
        verbose_name = 'AHU'

class TCO2(models.Model):
    class Meta:
        verbose_name = 'TCO2'
```

<br>

추가로 장고에서는 모델명을 복수로 (`verbose_name` + `s`) 나타내는데, 모델 복수명을 수정하고 싶다면 `verbose_name_plural`을 지정하면 된다.

ex) story 모델의 경우, `storys` -> `stories`

<br>

다시 확인해보니, 모델명이 잘 적용된 것을 볼 수 있다.

![모델명 지정 후](/no-access-please/assets/image/2022-02-08-how-to-change-the-default-table-name-in-the-admin-interface-in-django/2.png)

# 참고

[https://stackoverflow.com/questions/43239875/how-i-can-change-the-default-table-name-in-the-admin-interface-in-django](https://stackoverflow.com/questions/43239875/how-i-can-change-the-default-table-name-in-the-admin-interface-in-django)

[https://docs.djangoproject.com/en/3.2/ref/models/options/#verbose-name](https://docs.djangoproject.com/en/3.2/ref/models/options/#verbose-name)