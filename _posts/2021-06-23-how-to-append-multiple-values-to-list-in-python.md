---
layout: post
category: python
---

# 문제

파이썬 `list`에 한 개 이상에 value를 `append`하고 싶었다. 
뭔가 당연하게 `,`(comma)로 구분해 여러 value를 입력하면 될 거라고 생각했는데 오류가 발생했다. 😅

```python
fruit = []

fruit.append('apple', 'banana', 'orange') # ERROR
```

# 해결

`list`에 한 개 이상에 value를 `append`하고자 할 경우, `extend` 메소드를 사용해야 한다. 

```python
fruit = []

fruit.extend(['apple', 'banana', 'orange']) # ERROR
```

# 참고

[https://stackoverflow.com/questions/20196159/how-to-append-multiple-values-to-a-list-in-python/20196202](https://stackoverflow.com/questions/20196159/how-to-append-multiple-values-to-a-list-in-python/20196202){:target="_blank"}
