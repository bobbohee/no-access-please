---
layout: post
category: git
---

# 문제

Django(backend) + VueJS(frontend) 프로젝트에 pre-commit을 추가했다.

`exclude`에 작성된 디렉토리 또는 파일은 검사하지 않는데, frontend 디렉토리와 django의 migrations 디렉토리 등 1개가 아닌 여러 개를 검사에서 제외시키고 싶었다.

```text
📦 project
├─ backend
│  ├─ board
│  │  └─ migrations
│  └─ static
├─ frontend
├─ .gitignore
├─ .pre-commit-config.yaml
└─ README.md
```

<br>

공식 문서를 따라서 작성했는데, 검사에서 제외되지 않고 검사가 진행되었다.

👉 [https://pre-commit.com/#regular-expressions](https://pre-commit.com/#regular-expressions)

# 해결

정규 표현식 문법을 잘 몰라서 무슨 의미인지는 모르겠지만, 아래와 같이 작성하니 검사에서 제외되었다.

```yaml
exclude: |
    (?x)(
        ^frontend/|
        ^backend/static/|
        ^backend/board/migrations/
    )
```

# 참고

[https://github.com/psf/black/issues/395#issuecomment-499630129](https://github.com/psf/black/issues/395#issuecomment-499630129){:target="_blank"}
