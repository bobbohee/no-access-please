---
layout: post
category: odoo
---

# 문제 

#### 개발 환경
- `ubuntu` 18.04
- `python` 3.6.9
- `pip` 9.0.1

<br>

`requirements.txt`로 전역 설치를 하는데 `lxml`에서 무한 로딩이 걸리며 더 이상 설치가 진행되지 않았다.

# 원인

`requirements.txt`를 살펴보면 파이썬 버전에 따라 다른 `lxml` 버전을 설치하도록 되어있다.

```text
lxml==3.7.1 ; sys_platform != 'win32' and python_version < '3.7'
lxml==4.3.2 ; sys_platform != 'win32' and python_version >= '3.7'
lxml ; sys_platform == 'win32'
```

파이썬 3.6.9 버전에서는 `lxml 3.7.1` 버전이 설치되어야 하는데 어떤 문제 때문인지 설치가 진행되지 않는다. 

(Odoo의 issue에도 관련 내용이 올라왔지만 아무도 정확한 원인을 모른다.)

👉 [관련 issue 보기](https://github.com/odoo/odoo/issues/29556){:target="_blank"}

# 해결

나의 경우, `lxml 4.3.2`를 설치해도 무관하다고 판단해, `lxml 4.3.2` 버전을 설치했다.

```bash
pip3 install lxml=4.3.2
```

`lxml`을 따로 설치하고 다시 `requirements.txt`로 설치하는데 똑같이 lxml에서 설치에서 멈춘다면, `requirements.txt`에서 `lxml` 설치 부분은 잠시 삭제하고 다시 진행한다.
