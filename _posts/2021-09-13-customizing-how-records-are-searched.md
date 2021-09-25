---
layout: post
category: odoo
---

# 문제

Many2one 위젯에서 보여지는 이름에 다양한 필드 값을 나타내고 싶을 경우, `name_get()` 메소드를 사용한다.

예를 들어, 영화 테이블에 Many2one 위젯은 기본적으로는 영화 이름만 나타나게 되는데 영화 감독을 같이 나타내고 싶은 경우 아래와 같이 사용한다.

```python
def name_get(self):
    result = []
    for movie in self:
        name = '%s - %s' % (movie.name, movie.director) # 기생충 - 봉준호
        result.append((movie.id, name))
    return result
```

Many2one 위젯에서 영화 이름인 '기생충'만 보여지는 것이 아닌 '기생충 - 봉준호'로 나타난다.

<br>

문제는 Many2one 위젯에서 영화 이름 뿐만 아니라 영화 감독 이름으로도 영화를 검색하고 싶은 경우이다.

Many2one 위젯은 기본적으로 name 필드 (또는 _rec_name으로 지정한 필드) 값으로 검색을 한다.

# 해결

Many2one 위젯에서 여러 필드에서 검색하고 싶은 경우, `_name_search()` 메소드를 사용한다.
입력한 내용이 영화 이름 또는 영화 감독 이름과 일치하는지 검색하도록 검색 조건을 수정한다.

```python
@api.model
def _name_search(self, name='', args=None, operator='ilike', limit=100, name_get_uid=None):
    args = args or []
    if name:
        domain = ['|', ('name', operator, name), ('director', operator, name)]
        return self._search(expression.AND([domain, args]), limit=limit, access_rights_uid=name_get_uid)
    return super(Movie, self)._name_search(name=name, args=args, operator=operator, limit=limit, name_get_uid=name_get_uid)
```

# 참고

[https://subscription.packtpub.com/book/programming/9781800200319/5/ch05lvl1sec59/customizing-how-records-are-searched](https://subscription.packtpub.com/book/programming/9781800200319/5/ch05lvl1sec59/customizing-how-records-are-searched){:target="_blank"}

