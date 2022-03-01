---
layout: post
category: django
---

# 문제

SSL을 적용하지 않은 http 서버에서는 모든 것이 정상적으로 동작했는데, SSL을 적용한 https 서버에서는 Token을 넘겼음에도 아래와 같이 인증이 되지 않았다는 메세지가 나타났다.

```json
{
    "detail": "Authentication credentials were not provided."
}
```

참으로 기묘한 이야기...🎃

# 해결

Apache 설정 파일에 아래 설정을 추가하고, 재실행하니 Token 인증이 정상적으로 이루어졌다.

```
WSGIPassAuthorization on
```

# 참고

[https://stackoverflow.com/questions/66336931/django-drf-token-authentication-over-https-ssl](https://stackoverflow.com/questions/66336931/django-drf-token-authentication-over-https-ssl){:target="_blank"}
