---
layout: post
category: odoo
---

# 문제

`res.partner`를 검색하는 규칙 중 아래와 같은 규칙이 `base` 모듈에 정의되어 있었는데, 검색 조건을 변경하고 싶었다.

```xml
<record model="ir.rule" id="res_partner_rule">
    <field name="name">res.partner company</field>
    <field name="model_id" ref="base.model_res_partner"/>
    <!-- We exclude partners that have internal users (`partner_share` field) from
    the multi-company rule because it might interfere with the user's company rule
    and make some users unselectable in relational fields. This means that partners
    of internal users are always visible, not matter the company setting. -->
    <field name="domain_force">['|', '|', ('partner_share', '=', False), ('company_id', 'in', company_ids), ('company_id', '=', False)]</field>
</record>
```

# 해결

다른 모듈에 작성된 `ir.rule`을 상속받아, 재정의하고 싶은 경우에 `id`에 `{모듈명}.{아이디}`와 같이 정의하면 된다.

`base` 모듈에 `res_partner_rule` 규칙을 상속받고 싶은 경우 아래와 같이 작성하면 된다.

```xml
<record id="base.res_partner_rule" model="ir.rule">
    <field name="domain_force">['|', '&amp;', ('partner_share', '=', False), '|', ('company_id', 'in', company_ids), ('company_id', '=', False)]</field>
</record>
```


# 참고

[https://stackoverflow.com/questions/53030606/inherit-and-replace-ir-rule-odoo-11](https://stackoverflow.com/questions/53030606/inherit-and-replace-ir-rule-odoo-11){:target="_blank"}
