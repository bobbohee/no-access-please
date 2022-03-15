---
layout: post
category: python
---

# 문제

Django에서 아래와 같이 models 디렉토리를 생성해 모델 별로 파일을 분리해 모델을 작성하고, makemigrations 명령을 실행하니 아무런 변화가 일어나지 않았다.

```text
project
└─ dashboard (app)
   ├─ models
   │  ├─ __init__.py
   │  ├─ tco2.py
   │  └─ cer.py
   └─ __init__.py
```

<br>

알고보니 디렉토리 안에 모델을 위치한 경우, `models/__init__.py` 파일에서 모델을 import 해주어야 했다.

다시 makemigrations 명령을 실행하니, 모델이 정상적으로 생성되었다.

```
# models/__init__.py
from dashboard.models.tco2 import Tco2
from dashboard.models.cer import Cer
```

<br>

문제는 commit을 하니 `models/__init__.py`에서 flake8 오류가 발생했다.
오류의 내용은 클래스가 import 되었지만 사용되지 않았다는 내용이다.

```
'Tco2' imported but unused
'Cer' imported but unused
```

# 해결

### 방법1

아래 설정을 `.flake8` 파일에 추가해, `__init__.py` 파일은 flake8 검사를 하지 않도록 설정한다.

```
per-file-ignores = __init__.py:F401
```

### 방법2

`# noqa` 붙여, flake8 검사를 하지 않도록 설정한다.

```
from dashboard.models.tco2 import Tco2 # noqa
```

### 방법3

`__all__`에 import 한 클래스를 작성한다. 그렇게 되면 클래스 사용한 게 된다.

```
from dashboard.models.tco2 import Tco2
from dashboard.models.cer import Cer

__all__ = [
    'Tco2',
    'Cer',
]
```

# 참고

[https://stackoverflow.com/questions/8427701/how-to-ignore-pyflakes-errors-imported-but-unused-in-the-init-py-file](https://stackoverflow.com/questions/8427701/how-to-ignore-pyflakes-errors-imported-but-unused-in-the-init-py-file){:target="_blank"}

[https://stackoverflow.com/questions/31079047/python-pep8-class-in-init-imported-but-not-used/49266468](https://stackoverflow.com/questions/31079047/python-pep8-class-in-init-imported-but-not-used/49266468){:target="_blank"}
