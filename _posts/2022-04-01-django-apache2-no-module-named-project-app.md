---
layout: post
category: django 
---

# 문제

apache2에 django 배포 프로젝트를 위한 설정을 마치고, 사이트에 접속해보니 500 에러가 나타났다...🥲

로그를 확인해보니 config(프로젝트 App)을 찾을 수 없다는 내용이었다. 혹시나 하고 config 폴더가 없나 확인해보았지만, 역시나 있었다.

권한 문제일까?

```
// 생략
ModuleNotFoundError: No module named 'config'
```

# 해결

다행히 권한 문제는 아니었다... 휴... 

`config/wsgi.py` 파일에 아래 코드를 추가해주면 해결된다. `path`에는 프로젝트 경로를 작성한다.

```python
import sys

path = "/opt/project/GGMS"

if path not in sys.path:
    sys.path.append(path)
```
