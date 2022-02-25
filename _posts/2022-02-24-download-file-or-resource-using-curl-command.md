---
layout: post
category: terminal
---

# 문제

엑셀 다운로드 API를 개발을 마치고, 개발 문서에 개발 방법을 정리했다.
마지막으로 개발한 API를 curl로 테스트 해볼 수 있는 명령을 작성하기 위해, curl를 사용해 API를 테스트 해보니 Warning이 나타났다...! 😲

```
 curl \
-H "Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ0b2tlbl90eXBlIjoiYWNjZXNzIiwiZXhwIjoxNjQ1NjkzNzM1LCJpYXQiOjE2NDU2OTM0MzUsImp0aSI6IjkwY2NkYjg1YWYzMTQ4YmE4MDFjYzUzZDVlYmMyN2U5IiwidXNlcl9pZCI6MX0.H9cMQXwmBpEs1X3M20vOm_3jf2OBnPStNRfGBeeiTYY" \
http://localhost:8000/api/v1/excel/tco2/
Warning: Binary output can mess up your terminal. Use "--output -" to tell
Warning: curl to output it to your terminal anyway, or consider "--output
Warning: <FILE>" to save to a file.

```

# 해결

Warning을 자세히 읽어보니, 엑셀 파일을 바이너리로 출력하게 되면 터미널이 엉망이 되어 버리기 때문에 `--output`을 지정하라고 한다.

`--output` 또는 `-o` 뒤에 파일명을 작성하니 엑셀 파일이 나타났다. 🙆🏻

```
curl \
-H "Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ0b2tlbl90eXBlIjoiYWNjZXNzIiwiZXhwIjoxNjQ1NjkzNzM1LCJpYXQiOjE2NDU2OTM0MzUsImp0aSI6IjkwY2NkYjg1YWYzMTQ4YmE4MDFjYzUzZDVlYmMyN2U5IiwidXNlcl9pZCI6MX0.H9cMQXwmBpEs1X3M20vOm_3jf2OBnPStNRfGBeeiTYY" \
http://localhost:8000/api/v1/excel/tco2/ \
-o tco2.xlsx
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100  5047  100  5047    0     0   164k      0 --:--:-- --:--:-- --:--:--  164k

```

# 참고

[https://twpower.github.io/167-download-file-or-resource-using-curl-command](https://twpower.github.io/167-download-file-or-resource-using-curl-command){:target="_blank"}