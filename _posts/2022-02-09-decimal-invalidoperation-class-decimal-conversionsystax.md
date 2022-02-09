---
layout: post
category: python
---

# 문제

`django-import-export` 라이브러리를 활용해 admin 페이지에서 엑셀 데이터를 import 할 수 있도록 추가했다.

엑셀 데이터를 import 하니, 아래와 같이 `decimal`에서 오류가 발생했는데 오류가 발생한 원인을 알 수 없었다. 🙈

```text
decimal.InvalidOperation: [<class 'decimal.ConversionSyntax'>]
```

# 해결

열심히 검색해본 결과, 원인을 찾을 수 있었다.
위 오류는 `Decimal()`에 유효하지 않은 값을 전달한 경우에 발생한다.

```python
>>> from decimal import Decimal

>>> Decimal('34700')
Decimal('34700')

>>> Decimal('34,700')
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
decimal.InvalidOperation: [<class 'decimal.ConversionSyntax'>]
```

# 참고

[https://github.com/dateutil/dateutil/issues/632](https://github.com/dateutil/dateutil/issues/632){:target="_blank"}
