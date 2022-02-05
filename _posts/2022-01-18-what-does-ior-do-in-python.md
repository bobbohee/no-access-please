---
layout: post
category: python
---

Odoo 코어 모듈의 코드를 살펴보던 중, `|=` 연산자를 처음 보게 되었다.

조금 헷갈리는 부분이 있어 정리를 해두면 좋을 것 같아, 블로그에 정리하기로 했다.

# |= 연산자

`|=` 연산자는 병합(`|`) 및 업데이트(`|=`) 연산자이다.

sets, dicts, counters, numbers 타입에서 사용할 수 있다.

### sets

```python
>>> s1 = s1 | s2
>>> s1 |= s2
>>> s1.__ior__(s2)
```


```python
>>> s1 = {"a", "b", "c"}
>>> s2 = {"d", "e", "f"}

>>> s1 | s2
{'a', 'e', 'f', 'b', 'd', 'c'}
>>> s1
{'b', 'a', 'c'}

>>> s1 |= s2
>>> s1
{'a', 'e', 'f', 'b', 'd', 'c'}
```

### dicts

```python
>>> d1 = d1 | d2
>>> d1 |= d2
```

```python
>>> d1 = {"a": 0, "b": 1, "c": 2}
>>> d2 = {"c": 20, "d": 30}

>>> d1 | d2
{'a': 0, 'b': 1, 'c': 20, 'd': 30}
>>> d1
{'a': 0, 'b': 1, 'c': 2}

>>> d1 |= d2    # d1.update(d2) 와 동일하다
>>> d1
{'a': 0, 'b': 1, 'c': 20, 'd': 30}
```

##### ⚠️ 주의사항

dicts 타입에서는 3.9 이상의 버전에서만 사용이 가능하다.

만약 3.9 미만의 버전에서 사용하면 아래와 같은 오류가 발생한다.

```text
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: unsupported operand type(s) for |: 'dict' and 'dict'
```

### counters

```python
>>> c1 = c1 | c2
>>> c1 |= c2
```

```python
>>> import collections as ct
>>>
>>> c1 = ct.Counter({2: 2, 3: 3})
>>> c2 = ct.Counter({1: 1, 3: 5})

>>> c1 | c2
Counter({3: 5, 2: 2, 1: 1})
>>> c1
Counter({3: 3, 2: 2})

>>> c1 |= c2
>>> c1
Counter({3: 5, 2: 2, 1: 1})
```

### numbers

```python
>>> n1 = n1 | n2
>>> n1 |= n2
```

```python
>>> n1 = 0
>>> n2 = 1

>>> n1 | n2
1
>>> n1
0

>>> n1 |= n2
>>> n1
1
```


# 참고

[https://docs.python.org/3.9/whatsnew/3.9.html#dictionary-merge-update-operators](https://docs.python.org/3.9/whatsnew/3.9.html#dictionary-merge-update-operators){:target="_blank"}

[https://stackoverflow.com/questions/3929278/what-does-ior-do-in-python](https://stackoverflow.com/questions/3929278/what-does-ior-do-in-python){:target="_blank"}

[https://velog.io/@nayoon-kim/파이썬-연산자](https://velog.io/@nayoon-kim/%ED%8C%8C%EC%9D%B4%EC%8D%AC-%EC%97%B0%EC%82%B0%EC%9E%90){:target="_blank"}
