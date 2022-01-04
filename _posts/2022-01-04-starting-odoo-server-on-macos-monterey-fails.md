---
layout: post
category: odoo
---

# 문제

신규 입사자 분들에 odoo 설치를 도와드렸는데, 터미널에서 odoo 실행을 위한 명령어를 입력하니 `ValueError`가 발생하며 odoo가 실행되지 않았다.

검색해보니 macOS가 `Monterey`인 경우에 발생하는 오류라고 한다.

```bash
ValueError: current limit exceeds maximum limit
```

# 해결

odoo 실행을 위한 명령어에 `limit_memory_hard` 옵션을 추가하면 된다.

```bash
$ python ./odoo-bin --config=./config/.odoorc --limit-memory-hard 0
```

(디렉터리 구조는 아래와 같다.)

```text
|-- odoo-14
|   ├── addons
|   ├── config
|   │   └── .odoorc
|   ├── odoo-bin
// 일부 생략
```

<br>

또는 `.odoorc` 파일에 `limit_memory_hard` 옵션을 추가해도 된다.

```text
limit_memory_hard=0
```

# 참고

[https://github.com/odoo/odoo/issues/79112](https://github.com/odoo/odoo/issues/79112){:target="_blank"}