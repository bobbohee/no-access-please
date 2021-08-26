---
layout: post
category: odoo
---

# 문제

form 뷰에 안내 메시지를 HTML로 추가했다.

```xml
<xpath expr="//field[@name='purchase_origin_id']" position="after">
    <div class="alert alert-danger" role="alert" colspan="2">
        수입 검사는 해당 품목에 수입검사 관리점 등록과 요청, 수량 모두 입고되어야 합니다.
    </div>
</xpath>
```

<br>

여기서 문제는 조건에 따라 안내 메세지를 보여주고/숨기고 해야 하는데, `field` 태그가 아니라, 무슨 방법을 사용해야 할 지 감도 안 잡혔다...😔

Qweb에서 사용하는 `t-if`, `t-attf` 문법을 사용해봤지만, 아쉽게도 숨겨지지 않았다.

![안내 메세지 적용](/no-access-please/assets/image/2021-08-24-show-message-(html)-in-form-view-according-to-condition/1.png)

# 해결

`field` 태그에서 사용하는 것처럼 `attrs` 속성을 사용해 조건을 주면 된다.

```xml
<xpath expr="//field[@name='purchase_origin_id']" position="after">
    <div class="alert alert-danger" role="alert" colspan="2"
         attrs="{'invisible': [('purchase_origin_id', '==', False)]}">
        수입 검사는 해당 품목에 수입검사 관리점 등록과 요청, 수량 모두 입고되어야 합니다.
    </div>
</xpath>
```

<br>

당연히 `field` 태그에서 사용하는 odoo 속성을 사용할 수 없다고 생각해, odoo 속성은 배제하고 테스트를 해봤는데... 앞으로 섣부른 판단은 금지 ❌

# 참고

[https://www.odoo.com/es_ES/forum/ayuda-1/show-notification-warning-when-user-form-is-displayed-151560](https://www.odoo.com/es_ES/forum/ayuda-1/show-notification-warning-when-user-form-is-displayed-151560){:target="_blank"}
