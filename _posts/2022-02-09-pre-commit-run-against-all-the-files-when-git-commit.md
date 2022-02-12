---
layout: post
category: git
---

# 문제

Django 공식 문서의 [Coding Style](https://docs.djangoproject.com/en/dev/internals/contributing/writing-code/coding-style/){:target="_blank"}을 보면 `pre-commit`에 대한 내용이 있어
`pre-commit`을 설치하고, 실행해보니 아래와 같이 잘 동작했다.

```bash
$ pre-commit run -a
Trim Trailing Whitespace.................................................Failed
- hook id: trailing-whitespace
- exit code: 1
- files were modified by this hook

Fixing backend/board/management/commands/seed_board.py

Fix End of Files.........................................................Failed
- hook id: end-of-file-fixer
- exit code: 1
- files were modified by this hook

Fixing backend/board/views.py
Fixing backend/board/models.py

Check Yaml...............................................................Passed
Check for added large files..............................................Passed
```

<br>

위 명령은 테스트로 실행해본 것이기 때문에 위 명령 실행으로 인해 변경된 사항을 초기화 하고, 실 적용을 위해 commit을 해보니 위 명령을 실행했을 때와는 다르게 어떤 파일도 `Failed` 되지 않았다.

```bash
$ git commit -m "[ADD] pre-commit 추가"
 Trim Trailing Whitespace.................................................Passed
 Fix End of Files.........................................................Passed
 Check Yaml...............................................................Passed
 Check for added large files..............................................Passed
 [main 7008cfe] [ADD] pre-commit 추가
  4 files changed, 17 insertions(+), 3 deletions(-)
  create mode 100644 .pre-commit-config.yaml
```

# 해결

`pre-commit`은 commit을 했을 때, 모든 파일에 대해 검사를 하는 것이 아닌 변경 사항이 있는 파일만 검사한다.

`pre-commit run -a`는 모든 파일에 대해 검사를 해서 `Failed` 된 파일이 있었던 것이었고, commit을 했을 때는 변경된 파일에 대해 검사를 해 `Failed` 된 파일이 없었던 것이었다.

<br>

몇 시간 동안 이유를 찾았었는데 답은 공식 문서에 있었다... 이래서 공식 문서는 꼼꼼히 😓

# 참고

[https://pre-commit.com/#4-optional-run-against-all-the-files](https://pre-commit.com/#4-optional-run-against-all-the-files){:target="_blank"}
