---
layout: post
category: django
---

# 문제

Django의 ORM에서 값을 업데이트(수정) 하기 위해 아래 코드와 같이 `update`를 사용했다.

```python
Entry.objects.get(pk=pk).update(comments_on=True)
```

<br>

확인을 해보니 `Entry` 객체에 `update`가 없다는 오류가 발생했다. 🤔???

```text
AttributeError: 'Entry' object has no attribute 'update'
```

# 해결

이래서 공식 문서를 잘 읽어봐야 한다...

`get`을 사용해 값을 없데이트 할 경우에는 `update`를 사용할 수 없고, 아래 코드와 같이 값을 업데이트 해야 한다.

```python
e = Entry.objects.get(pk=pk)
e.comments_on = True
e.save()
```

<br>

`filter`를 사용한 경우에는 아래 코드와 같이 `update`를 사용할 수 있다.

```python
Entry.objects.filter(pk=pk).update(comments_on=True)
```

<br>

`get`은 검색 결과에 해당하는 하나의 객체를 반환하고, `filter`는 검색 결과에 해당하는 여러 개의 객체를 포함한 `QuerySet`을 반환한다.

# 참고

[https://docs.djangoproject.com/en/4.0/ref/models/querysets/#update](https://docs.djangoproject.com/en/4.0/ref/models/querysets/#update){:target="_blank"}