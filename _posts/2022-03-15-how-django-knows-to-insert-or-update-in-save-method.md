---
layout: post
category: django
---

# 문제

Django에서는 데이터 추가(insert) 및 수정(update) 시, `save` 메소드를 이용한다.

데이터 추가 및 수정 시에 유저를 기록해야 해서 `save` 메소드에서 데이터를 추가하는 경우인지, 수정하는 경우인지 구분해야 했다.

```python
def save(self, *args, **kwargs):
    is_create = None # 어떤 값을 넣어야 할까
    username = get_current_user().username
    if is_create:
        self.create_user = username
    self.update_user = username
    return super(AbstractLogging, self).save(*args, **kwargs)
```

# 해결

### 방법1

제일 많이 사용하는 방법으로 pk 값이 있는지 확인해, 데이터에 pk 값이 없다면 `추가(insert)`, pk 값이 있다면 `수정(update)`으로 판단한다.

```python
is_create = not self._get_pk_val()
```

<br>

⚠️ 이 방법에 문제는 아래와 같이 pk가 자동 생성되는 AutoField가 아닌, 따로 pk 필드를 선언해 데이터 추가 시에 pk 데이터도 포함하는 경우라면 사용할 수 없다.

```
class Book(models.Model):
    isbn = models.CharField(primary_key=True, max_length=20)
    name = models.CharField(primary_key=True, max_length=50)
```

### 방법2

방법1보다는 방법2를 사용하는 것이 더 안전하다.

```python
is_create = self._state.adding
```

# 참고

[https://stackoverflow.com/questions/907695/in-a-django-model-custom-save-method-how-should-you-identify-a-new-object](https://stackoverflow.com/questions/907695/in-a-django-model-custom-save-method-how-should-you-identify-a-new-object)

[https://stackoverflow.com/questions/57459259/does-djangos-save-create-or-update](https://stackoverflow.com/questions/57459259/does-djangos-save-create-or-update)
