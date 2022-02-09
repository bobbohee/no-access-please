---
layout: post
category: python
---

# 방법

`requirements.txt` 파일은 python 프로젝트에 필요한 패키지 정보가 담긴 파일이다.

아래 명령을 실행하면 설치된 패키지 목록이 자동으로 `requirements.txt` 파일로 생성된다.

```bash
pip freeze > requirements.txt
```

<br>

아래 명령을 실행하면 `requirements.txt` 파일에 패키지가 일괄로 설치된다.

```bash
$ pip install -r requirements.txt
```

# 참고

[https://stackoverflow.com/questions/31684375/automatically-create-requirements-txt](https://stackoverflow.com/questions/31684375/automatically-create-requirements-txt){:target="_blank"}