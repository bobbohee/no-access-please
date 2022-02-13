---
layout: post
category: django
---

# 문제

장고(Django) 강의를 수강하면서 모델 선언 시 `__str__` 함수를 작성하는 이유가 궁금해졌다.

`__str__` 함수는 객체를 print 할 경우에 반환할 문자열을 리턴하는 것으로 알고 있는데, 장고에서는 아래 코드와 같이 필드를 리턴해주고 있어 어떠한 이유로 작성하는지 궁금했다.

```python
class Carbon(models.Model):
    name = models.CharField(max_length=30)
    created_at = models.DateTimeField(auto_now_add=True)
    updated_at = models.DateTimeField(auto_now=True)
    # code...

    def __str__(self):
        return self.name
```

# 해결

장고에서 모델 선언 시 `__str__` 함수를 작성하는 이유는 관리자 페이지에서 레코드 명을 설정하기 위해서이다.

<br>

`__str__` 함수를 작성하지 않으면 레코드 명이 아래와 같이 나타나 레코드를 구분하기가 어렵다. 🙅🏻

![str 함수 작성 전](/no-access-please/assets/image/2022-02-08-what-is-doing-str-function-in-django/1.png)

<br>

`__str__` 함수를 작성해 필드 값을 레코드 명을 설정해놓으면 레코드를 구분하기가 쉬워진다. 🙆🏻

![str 함수 작성 후](/no-access-please/assets/image/2022-02-08-what-is-doing-str-function-in-django/2.png)




# 참고

[https://stackoverflow.com/questions/45483417/what-is-doing-str-function-in-django](https://stackoverflow.com/questions/45483417/what-is-doing-str-function-in-django){:target="_blank"}