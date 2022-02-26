---
layout: post
category: django
---

# 문제

EC2에 장고 서버를 배포하고 swagger 페이지를 확인해보니 `Django Login` 링크만 나타났다.

`DEFAULT_AUTHENTICATION_CLASSES`를 설정했기 떄문에, 로그인을 해야 페이지를 확인할 수 있는 줄 알고 로그인을 한 후에 다시 페이지를 확인해보니 똑같았다.

(`DEFAULT_AUTHENTICATION_CLASSES`을 설정한 것과는 관련이 없었다...ㅎㅎ)

# 해결

아래 명령을 실행해 static 폴더를 다시 생성하니 해결되었다.

```
python manage.py collectstatic
```

# 참고

[https://stackoverflow.com/questions/62031565/how-to-disable-django-login-page-when-trying-to-access-swagger-api-in-browser](https://stackoverflow.com/questions/62031565/how-to-disable-django-login-page-when-trying-to-access-swagger-api-in-browser){:target="_blank"}