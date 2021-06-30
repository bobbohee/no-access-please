---
layout: post
category: odoo
---

# 문제

관리자만 볼 수 있게, 관리자만 수정할 수 있게, 관리자만 선택할 수 있게 ... 등 특정 유저(꼭! 관리자가 아니라도)만 가능하도록 하고 싶은 경우가 있다.

그 중 사용자에 따라 보여지고, 숨겨지고를 가장 많이 사용하는데 `groups` 속성을 사용하면 해당 그룹에 사용자만 필드를 볼 수 있도록 설정할 수 있다.

<br>

ex) `base.group_erp_manager` 그룹에 사용자만 `vat` 필드를 볼 수 있다.
```xml
<field name="vat" groups="base.group_erp_manager"/>
```

<br>

문제는 관리자 그룹에 사용자만 필드 수정이 가능하고, 그 외 사용자는 `readonly`여야 하는데, `groups` 속성으로는 특정 그룹에 사용자만 필드 수정이 가능하도록 할 수 없다.

# 해결

## 조금 지저분한(?) 방법

관리자 그룹임을 체크하는 필드를 하나 생성해, 해당 필드로 관리자 그룹임을 판단한다.

<br>

**view(xml)**

```xml
<field name="check_field" invisible="1"/>
<field name="vat" attrs="{'readonly': [('check_field', '!=', True)]}"/>
```

**model(python)**

```python
check_field = fields.Boolean('Check', compute='get_user')

@api.depends('new_field')   
def get_user(self):
    if SUPERUSER_ID == self._uid:
        self.check_user = True    
   else:
        self.check_user = False
```

## 깔끔한 방법

기본적으로 모든 사용자가 필드를 수정하지 못하도록 `readonly`를 True로 설정한다.

```xml
 <record id="view_template_form_A" model="ir.ui.view">
    <field name="name">product.template</field>
    <field name="model">product.template</field>
    <field name="inherit_id" ref="product.view_template_form"/>
    <field name="arch" type="xml">
        <xpath expr="//field[@name='vat']" position="attributes">
            <attribute name="readonly">True</attribute>
        </xpath>
    </field>
</record>
```

<br>

`groups_id` 속성을 사용해 해당 그룹에 사용자만 해당 뷰를 적용하도록 한다.

`base.group_erp_manager` 그룹에 사용자만 해당 뷰가 적용되기 때문에, `readonly`를 False로 설정한다.

```xml
 <record id="view_template_form_B" model="ir.ui.view">
    <field name="name">product.template</field>
    <field name="model">product.template</field>
    <field name="groups_id" ref="[(6, 0, [ref('base.group_erp_manager')])]"/>
    <field name="inherit_id" ref="custom_product.view_template_form_A"/>
    <field name="arch" type="xml">
        <xpath expr="//field[@name='vat']" position="attributes">
            <attribute name="readonly">False</attribute>
        </xpath>
    </field>
</record>
```

# 참고

[https://www.odoo.com/fr_FR/forum/aide-1/how-to-set-a-field-editable-only-for-a-group-in-odoo9-107563](https://www.odoo.com/fr_FR/forum/aide-1/how-to-set-a-field-editable-only-for-a-group-in-odoo9-107563){:target="_blank"}

[https://www.odoo.com/es_ES/forum/ayuda-1/how-to-make-field-read-only-except-administrative-user-in-odoo-115807](https://www.odoo.com/es_ES/forum/ayuda-1/how-to-make-field-read-only-except-administrative-user-in-odoo-115807){:target="_blank"}
