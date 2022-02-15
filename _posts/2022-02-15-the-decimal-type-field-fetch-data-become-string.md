---
layout: post
category: django
---

# 문제

장고의 DRF(django-rest-framework)를 이용해 개발한 API를 확인해보니 `tco2` 데이터가 숫자형 타입이 아닌 문자열로 나타났다.

```json
{
    "id": 537,
    "tco2": "207.4", // 👈
    "reference_date": "2022-02-15"
},
```

<br>

`DecimalField`로 선언을 했는데, 왜 문자열로 나타나는지 의문이었다. 🤔

```python
class TCO2(models.Model):
    """ 일일 온실가스 배출량 """
    tco2 = models.DecimalField(max_digits=4, decimal_places=1, verbose_name='tCO2')
    reference_date = models.DateField()
```

# 해결

왜 문자열로 나타나는지에 대한 이유를 찾지는 못했지만 숫자형 타입으로 나타낼 수 있는 방법을 찾았다.

## 방법1. 전역 설정

`settings.py`에 설정하면, `DecimalField`로 선언된 모든 필드에 적용된다.

```python
REST_FRAMEWORK = {
    'COERCE_DECIMAL_TO_STRING': False,
    # other settings
}
```

## 방법2. 필드별 설정

`coerce_to_string=False`로 설정하면, 필드 별로 적용할 수 있다.

```python
class TCO2(models.Model):
    tco2 = models.DecimalField(coerce_to_string=False, max_digits=4, decimal_places=1, verbose_name='tCO2')
```

<br>

방법1을 적용하고 확인해보니, 문자열이 아닌 숫자형 타입으로 나타났다. 👏

```json
{
    "id": 537,
    "tco2": 207.4, // 👈
    "reference_date": "2022-02-15"
},
```

# 참고

[https://www.django-rest-framework.org/api-guide/fields/#decimalfield](https://www.django-rest-framework.org/api-guide/fields/#decimalfield)

[https://stackoverflow.com/questions/49770344/the-decimal-type-field-fetch-data-become-string](https://stackoverflow.com/questions/49770344/the-decimal-type-field-fetch-data-become-string)
