---
layout: post
category: odoo
---

# 문제

Odoo의 기존 메뉴의 새로운 메뉴를 추가했다. 근데 메뉴가 보이지 않았다. 

모듈 정보에 들어가 생성된 메뉴를 보니, 정상적으로 메뉴는 추가된 것을 확인할 수 있었다. 🤔

![모듈 정보의 생성된 메뉴](/no-access-please/assets/image/2021-07-08-how-to-add-menu-item-to-existing-menu/1.png)

# 해결

알고보니 모델에 대한 보안 규칙을 추가해줘야 됐다. CRUD 권한이 없다면 사실상 메뉴를 보여줄 필요도 없기 떄문에..!

보안 규칙을 추가하기 전, 그저 메뉴가 잘 추가되었는지만 확인하고 싶다면 개발자 모드에서 슈퍼 유저를 활성화하면 메뉴가 나타난다.

![슈퍼 유저 되기](/no-access-please/assets/image/2021-07-08-how-to-add-menu-item-to-existing-menu/2.png)

# 참고

[https://www.odoo.com/es_ES/forum/ayuda-1/how-to-add-menu-item-to-sales-menu-51405](https://www.odoo.com/es_ES/forum/ayuda-1/how-to-add-menu-item-to-sales-menu-51405){:target="_blank"}
