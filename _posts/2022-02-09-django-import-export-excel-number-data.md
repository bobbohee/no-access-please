---
layout: post
category: django
---

# 문제

`django-import-export` 라이브러리를 활용해 admin 페이지에서 엑셀 데이터를 import 할 수 있도록 추가했다.

아래와 같은 엑셀 데이터를 import 하니, 오류가 발생하며 엑셀 데이터가 import 되지 않았다.

| base_time  | name  | close_price | day_over_day | range | ... |
|------------|-------|-------------|--------------|-------|-----|
| 2022-02-09 | KAU21 | 34,300      | -350         | -1.01 | ... |
| 2022-02-09 | KAU22 | 32,700      | 0            | 0.00  | ... |

```text
Line number: 1 - [<class 'decimal.ConversionSyntax'>]
2022-02-09, KAU21, 34,300, -350, 0.0, 34,650, 34,650, 34,300, 24,200, 834,830,000, 34,497
Traceback (most recent call last):
File "/Users/bobbohee/.pyenv/versions/hw_esg/lib/python3.8/site-packages/import_export/resources.py", line 691, in import_row
self.import_obj(instance, row, dry_run, **kwargs)
File "/Users/bobbohee/.pyenv/versions/hw_esg/lib/python3.8/site-packages/import_export/resources.py", line 541, in import_obj
self.import_field(field, obj, data, **kwargs)
File "/Users/bobbohee/.pyenv/versions/hw_esg/lib/python3.8/site-packages/import_export/resources.py", line 524, in import_field
field.save(obj, data, is_m2m, **kwargs)
File "/Users/bobbohee/.pyenv/versions/hw_esg/lib/python3.8/site-packages/import_export/fields.py", line 110, in save
cleaned = self.clean(data, **kwargs)
File "/Users/bobbohee/.pyenv/versions/hw_esg/lib/python3.8/site-packages/import_export/fields.py", line 66, in clean
value = self.widget.clean(value, row=data, **kwargs)
File "/Users/bobbohee/.pyenv/versions/hw_esg/lib/python3.8/site-packages/import_export/widgets.py", line 88, in clean
return int(Decimal(value))
decimal.InvalidOperation: [<class 'decimal.ConversionSyntax'>]
```

# 해결

오류는 `Decimal()`에 유효하지 않은 값을 전달한 경우에 발생하는 오류로 따로 정리를 해두었다.

👉 [파이썬 decimal.InvalidOperation: [<class 'decimal.ConversionSyntax'>] 오류](/no-access-please/decimal-invalidoperation-class-decimal-conversionsystax)

## #1

오류가 발생한 원인을 알게되고, 엑셀에 데이터를 확인해보니 데이터 서식에 문제가 있었다.

`C2`를 클릭해보면 상단에 `34,300`이라는 데이터가 나타난다.

![엑셀 숫자 데이터 1](/no-access-please/assets/image/2022-02-09-django-import-export-excel-number-data/1.png)

`Decimal('34,300')`을 실행해보면 ,(콤마)로 인해 오류가 발생해 ,(콤마)를 제거해야 한다.

```python
>>> from decimal import Decimal

>>> Decimal('34,300')
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
decimal.InvalidOperation: [<class 'decimal.ConversionSyntax'>]
```

## #2

서식을 변경하기 위해 ⚠️ 아이콘을 클릭한다.

![엑셀 숫자 데이터 2](/no-access-please/assets/image/2022-02-09-django-import-export-excel-number-data/2.png)

## #3

숫자로 변환을 클릭해 텍스트 서식에서 숫자 서식으로 변경한다.

![엑셀 숫자 데이터 3](/no-access-please/assets/image/2022-02-09-django-import-export-excel-number-data/3.png)

## #4

다시 `C2`를 클릭해보면 ,(콤마)가 제거되어 `34300`이라는 데이터가 나타나는 것을 확인할 수 있다.

![엑셀 숫자 데이터 4](/no-access-please/assets/image/2022-02-09-django-import-export-excel-number-data/4.png)
