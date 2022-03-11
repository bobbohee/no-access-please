---
layout: post
category: django
---

# 문제

아래 예시와 같이 1개의 검색 입력폼을 두고, 여러 필드를 검색하고 싶은 경우에 `django-filter`에서 어떻게 필터링 어떻게 할 지 고민했다.

`django-filter`를 사용하지 않고, 직접 queryset을 필터링 하는 방법도 있지만, 검색 파라미터를 따로 처리하게 되기 때문에 유지보수 측면에서 좋지 않을 것 같아, 되도록 `django-filter`를 사용해 처리하고 싶었다.

![여러 필드 검색 예시](/no-access-please/assets/image/2022-03-11-how-to-make-multiple-fields-search-with-django-filter/1.png)

# 해결

method를 선언해 method에서 `Q`를 사용해 `or` 조건으로 검색하니, 여러 필드에서 검색되도록 처리할 수 있었다.

```python
from django.db.models import Q
import django_filters

from company.models import Employee


class CERFilter(django_filters.FilterSet):
    search = django_filters.NumberFilter(method='search_filter')

    class Meta:
        model = Employee
        fields = ['search']

    def search_filter(self, queryset, name, value):
        return queryset.filter(Q(name=value) | Q(job_title=value))
```

# 추가

[https://stackoverflow.com/questions/57270470/django-filter-how-to-make-multiple-fields-search-with-django-filter](https://stackoverflow.com/questions/57270470/django-filter-how-to-make-multiple-fields-search-with-django-filter)