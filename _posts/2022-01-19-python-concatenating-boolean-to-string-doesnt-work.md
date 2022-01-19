---
layout: post
category: python
---

# 문제

odoo 교육에서 name_get() 메소드에 대해 설명하고, 결과를 확인해보기 위해 레코드를 클릭하니 오류가 발생했다.

```python
def name_get(self):
    result = []
    for record in self:
        rec_name = '[' + record.album_id.name + '] ' + record.name
        result.append((record.id, rec_name))
    return result
```

```text
TypeError: can only concatenate str (not "bool") to str
```

<br>

해당 레코드에는 앨범(`album_id`)을 설정하지 않아, `record.album_id.name`이 False 값이다 보니, string 타입과 boolean 타입을 더할 수 없어서 발생한 오류였다.

```python
rec_name = '[' + record.album_id.name + '] ' + record.name
# rec_name = '[' + False + '] ' + record.name
```

# 해결

### 방법1

앨범(`record.album_id`) 값이 설정된 경우와 없을 설정되지 않은 경우를 다르게 처리한다.

```python
if record.album_id:
    rec_name = "[%s] %s" % (record.album_id.name, record.name)
else:
    rec_name = record.name

# 설정된 있는 경우 : [신사와 아가씨 OST Part.2] 사랑은 늘 도망가
# 설정되지 않은 경우 : 사랑은 늘 도망가
```

### 방법2

boolean 타입에 False를 string 타입으로 변환하여 오류가 발생하지 않도록 한다.
(좋은 방법은 아니다.)

```python
rec_name = '[' + str(record.album_id.name) + '] ' + record.name
rec_name = "[%s] %s" % (record.album_id.name, record.name)

# [False] 사랑은 늘 도망가
```

# 참고

[https://stackoverflow.com/questions/46903676/python-concatenating-boolean-to-string-doesnt-work](https://stackoverflow.com/questions/46903676/python-concatenating-boolean-to-string-doesnt-work){:target="_blank"}
