---
layout: post
category: django
---

# 문제

API를 요청하니 console에 아래와 같이 Warning 메세지가 나타났다...😲

처음에는 오류 메세지인 줄 알고 식겁했지만 다행히(?) 경고 메세지였다. 오류 메세지가 아니라고 무시하면 안되는 법! 경고 메세지가 발생한 이유와 해결 방법을 찾아보기로 했다.

```
.../rest_framework/pagination.py:200: UnorderedObjectListWarning: Pagination may yield inconsistent results with an unordered object_list: <class 'dashboard.models.CER'> QuerySet.
  paginator = self.django_paginator_class(queryset, page_size)
[24/Feb/2022 15:13:15] "GET /api/v1/excel/ HTTP/1.1" 200 6195
```

# 해결

Warning 타입을 보면, `UnorderedObjectListWarning`으로 order(순서)와 관련된 것임을 알 수 있다.

model 또는 queryset에 order를 지정해주면 해결된다.

### model

```
class CER(models.Model):

    class Meta:
        ordering = ['-id']
```

### queryset

```
class CERViewSet(viewsets.ModelViewSet):

    queryset = models.CER.objects.all().order_by('-id')
    serializer_class = serializers.CERSerializer
```

# 참고

[https://stackoverflow.com/questions/44033670/python-django-rest-framework-unorderedobjectlistwarning](https://stackoverflow.com/questions/44033670/python-django-rest-framework-unorderedobjectlistwarning){:target="_blank"}