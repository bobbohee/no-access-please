---
layout: post
category: django
---

# 문제

장고의 DRF(django-rest-framework)를 이용해 API를 개발하고 있었다.
그러다 내가 원하는 json 데이터를 리턴하고 싶어 DRF를 사용하지 않고, 장고의 `View`와 `JsonResponse`를 사용해 데이터를 리턴했다.

```python
from django.views import View
from django.http import JsonResponse


class TestView(View):
    def get(self, request):
        return JsonResponse({
            'some': 'data',
            'code': 200
        })
```

<br>

위 코드를 실행해보니, 아래와 같이 텍스트만 나타났다. DRF를 이용하면 API를 실행할 수 있는 화면과 기능을 제공하는데, DRF를 이용하지 않으니 텍스트만 나타나 통일성도 없을 뿐더러 보기 불편했다.

![URL 접속 시 나타나는 화면 1](/no-access-please/assets/image/2022-02-11-how-to-return-custom-json-in-django-rest-framework/1.png)

# 해결

장고의 DRF에서 내가 원하는 json 데이터를 리턴하고 싶은 경우, DRF의 `APIView`와 `Response`를 이용해 데이터를 리턴하면 된다.

```python
from rest_framework.views import APIView
from rest_framework.response import Response


class TestView(APIView):
    def get(self, request):
        return Response({
            'some': 'data',
            'code': 200
        })
```

<br>

다시 실행해보니 이번에는 DRF의 API 실행할 수 있는 화면이 생겼다!

![URL 접속 시 나타나는 화면 2](/no-access-please/assets/image/2022-02-11-how-to-return-custom-json-in-django-rest-framework/2.png)

# 참고

[https://stackoverflow.com/questions/35019030/how-to-return-custom-json-in-django-rest-framework](https://stackoverflow.com/questions/35019030/how-to-return-custom-json-in-django-rest-framework){:target="_blank"}

[https://ssungkang.tistory.com/entry/Django-APIView-Mixins-generics-APIView-ViewSet을-알아보자](https://ssungkang.tistory.com/entry/Django-APIView-Mixins-generics-APIView-ViewSet%EC%9D%84-%EC%95%8C%EC%95%84%EB%B3%B4%EC%9E%90){:target="_blank"}