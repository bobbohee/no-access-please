---
layout: post
category: django
---

# 차이점

## LimitOffsetPagination

Query Parameter로 `limit`과 `offset`을 사용한다.

```text
GET /api/v1/cer/?offset=60
```

```json
{
    "count": 220,
    "next": "http://127.0.0.1:8000/api/v1/cer/?limit=30&offset=90",
    "previous": "http://127.0.0.1:8000/api/v1/cer/?limit=30&offset=30",
    "results": []
}
```

## PageNumberPagination

Query Parameter로 `page`를 사용한다.

```text
GET /api/v1/cer/?page=3
```

```json
{
    "count": 220,
    "next": "http://127.0.0.1:8000/api/v1/cer/?page=4",
    "previous": "http://127.0.0.1:8000/api/v1/cer/?page=2",
    "results": []
}
```

# 참고

[https://www.django-rest-framework.org/api-guide/pagination](https://www.django-rest-framework.org/api-guide/pagination)

[https://donis-note.medium.com/django-rest-framework-pagination-페이징-처리-f97aaf824433](https://donis-note.medium.com/django-rest-framework-pagination-%ED%8E%98%EC%9D%B4%EC%A7%95-%EC%B2%98%EB%A6%AC-f97aaf824433)