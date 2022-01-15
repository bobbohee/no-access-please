---
layout: post
category: javascript
---

# 문제

string을 boolean 타입으로 변경할 때, 문자열이 있냐 없냐로 true, false가 된다.

```javascript
Boolean('')                  // false
Boolean('hello world')  // true
```

<br>

내가 궁금했던 것 문자열 `'true'`, `'false'`를 boolean 타입으로 변경할 수 있는 방법이었다.
`Boolean()` 메소드를 사용하게 되면 문자열이 있으니 둘 다 true가 된다.

```javascript
Boolean('true')    // true
Boolean('false')  // true
```

# 해결

`JSON.parse()`를 사용하면 된다.

```javascript
JSON.parse('true')    // true
JSON.parse('false')  // false
```

<br>

`JSON.parse()` 사용 시 주의할 점은 `true`가 아닌 `True`, `TRUE`는 오류가 발생한다. (false도 마찬가지이다.)

그럴 경우 모두 소문자로 변환해야 한다.

```javascript
JSON.parse('True')                  // SyntaxError
JSON.parse('True'.toLowerCase())    // true
```

# 참고

[https://stackoverflow.com/questions/263965/how-can-i-convert-a-string-to-boolean-in-javascript](https://stackoverflow.com/questions/263965/how-can-i-convert-a-string-to-boolean-in-javascript){:target="_blank"}

[https://reference-m1.tistory.com/179](https://reference-m1.tistory.com/179){:target="_blank"}
