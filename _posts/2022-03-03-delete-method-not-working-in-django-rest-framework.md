---
layout: post
category: django
---

# 문제

DRF를 이용해 파일 API를 개발하고, 삭제 테스트를 해보기 위해 DELETE 메소드로 API를 호출했다.
결과로 삭제되어야 할 레코드 정보를 반환하길래 데이터베이스를 확인해보니 레코드가 삭제되지 않았다.

```text
DELETE http://127.0.0.1:8000/api/v1/file/7
```

```json
{
    "id": 7,
    "name": "cer_20220303",
    "file": "http://127.0.0.1:8000/media/cer_20220303.xls",
    "create_at": "2022-03-03T18:06:42.928086"
}
```

<br>

Postman이 문제인가 싶어 console을 확인해보니 DELETE 메소드로 잘 요청이 들어오고 있었다. 근데 DELETE 요청 시, GET 메소드가 자동으로 요청하고 있었다. 🤔 ???

그래도 DELETE로 먼저 요청이 들어오고, GET으로 요청이 되는데 삭제는 되어야 하는 거 아닌가? 하고 삭제 동작을 하는 메소드에 debug를 걸어보았는데, debug에 걸리지 않았다.

```text
[03/Mar/2022 18:07:17] "DELETE /api/v1/file/7 HTTP/1.1" 301 0
[03/Mar/2022 18:07:17] "GET /api/v1/file/7/ HTTP/1.1" 200 125
```

# 해결

검색해도 도통 해결 방법을 찾을 수 없었는데, 알고보니 맨 뒤에 붙는 `/(slash)`가 없어서 그런 것이었다...

`/`를 붙여 다시 요청하니 정상적으로 삭제 처리가 되었다.

```text
DELETE http://127.0.0.1:8000/api/v1/file/7/
```