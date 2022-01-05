---
layout: post
category: odoo
---

# 문제

odoo-bin 파일을 실행하니 cli 관련 오류가 발생했다.
웬만한 오류를 다 겪어봤다고 생각했는데, 이건 아무리 검색해봐도 해결 방법을 찾을 수 없었다.

```bash
$ python odoo-bin --save
```

```bash
Traceback (most recent call last):
  File “./odoo-bin”, line 8, in <module>
    odoo.cli.main()
AttributeError: module ‘odoo’ has no attribute ‘cli’
```

# 해결

cli 모듈을 가져오지 못해 발생하는 오류라 `__init__.py` 파일을 살펴보려 했는데 `__init__.py` 파일이 없었다.
알고보니 odoo 프로젝트를 복사해 다른 폴더로 붙여넣는 과정에서 전체 모듈의 `__init__.py` 및 `__manifest__.py` 파일이 날라가버린 것이다.
그래서 누락된 파일을 넣어주니 정상적으로 동작했다. ...😲