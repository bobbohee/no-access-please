---
layout: post
category: odoo
---

# 문제

[How To Inherit Ir Rule In Odoo](/no-access-please/how-to-inherit-ir-rule-in-odoo){:target="_blank"} 에 정리해 놓은 것과 같이 커스텀 모듈에 규칙을 재정의하고, 커스텀 모듈을 업데이트 했지만, 규칙이 업데이트 되지 않았다.

```xml
<?xml version="1.0" encoding="utf-8"?>
<odoo>
    <data>
        <record id="base.res_partner_rule" model="ir.rule">
            <field name="domain_force">['|', '&amp;', ('partner_share', '=', False), ('partner_share', '!=', None), '|', ('company_id', 'in', company_ids), ('company_id', '=', False)]</field>
        </record>
    </data>
</odoo>
```

# 해결

규칙이 업데이트 되지 않은 이유는 `<data noupdate="1">` 때문이었고, `noupdate`가 설정되지 않은 경우에는 업데이트가 정상적으로 이루어졌다.

상속받은 모듈의 `noupdate` 옵션을 비활성화하는 코드를 먼저 삽입해 `noupdate` 옵션을 비활성화하고, 규칙을 업데이트했다.

```xml
<?xml version="1.0" encoding="utf-8"?>
<odoo>
    <data>
        <function name="write" model="ir.model.data">
            <function name="search" model="ir.model.data">
                <value eval="[('module', '=', 'base'), ('name', '=', 'res_partner_rule')]" />
            </function>
            <value eval="{'noupdate': False}" />
        </function>

        <record id="base.res_partner_rule" model="ir.rule">
            <field name="domain_force">['|', '&amp;', ('partner_share', '=', False), ('partner_share', '!=', None), '|', ('company_id', 'in', company_ids), ('company_id', '=', False)]</field>
        </record>

        <function name="write" model="ir.model.data">
            <function name="search" model="ir.model.data">
                <value eval="[('module', '=', 'base'), ('name', '=', 'res_partner_rule')]" />
            </function>
            <value eval="{'noupdate': True}" />
        </function>
    </data>
</odoo>
```

# 참고

[https://www.odoo.com/ko_KR/forum/doummal-1/how-to-inherit-and-change-the-domain-of-standard-rules-in-odoo-8-0-69326](https://www.odoo.com/ko_KR/forum/doummal-1/how-to-inherit-and-change-the-domain-of-standard-rules-in-odoo-8-0-69326){:target="_blank"}
