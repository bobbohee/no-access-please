---
layout: post
category: python
---

# 문제

파이썬의 `datetime` 또는 `date`를 사용해서 지난 달을 어떻게 구할까 ?

# 해결

방법은 생각보다 간단했다.

<br>

현재 날짜를 가져와 일을 1일로 변경하고, 1일을 빼면 지난 달 날짜를 가져올 수 있었다.

```python
from datetime import date, timedelta

today = date.today()    # datetime.date(2022, 2, 14)
one_day = timedelta(days=1)
last_date = today.replace(day=1) - one_day  # datetime.date(2022, 1, 31)
last_month = last_date.month    # 1
```

<br>

보기 좋진 않지만, 1줄로도 작성할 수 있다.

```python
last_month = (date.today().replace(day=1) - timedelta(days=1)).month    # 1
```

# 참고

[https://stackoverflow.com/questions/9724906/python-date-of-the-previous-month](https://stackoverflow.com/questions/9724906/python-date-of-the-previous-month){:target="_blank"}