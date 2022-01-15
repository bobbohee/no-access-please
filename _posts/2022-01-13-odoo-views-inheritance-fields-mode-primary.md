---
layout: post
category: odoo
---

# 문제

각 공정별로 공정 이동표 뷰를 작성하는데 alert 메세지와 footer가 공통적으로 사용되어 alert 메세지와 footer를 공통 뷰를 만들고, 각 공정 이동표 뷰에서 공통 뷰를 상속받아 필드를 추가하기로 했다.

```xml
<record id="lotsheet_lotsheet_routing_view_form" model="ir.ui.view">
    <field name="name">lotsheet.lotsheet.routing.form</field>
    <field name="model">lotsheet.lotsheet</field>
    <field name="arch" type="xml">
        <form>
            <sheet>
                <div class="alert alert-info" role="alert">You can fill out the lotsheet once for each work order.</div>
            </sheet>
            <footer>
                <button string="Save And Close" class="btn-primary" special="save"/>
                <button string="Cancel" class="btn-secondary" special="cancel"/>
            </footer>
        </form>
    </field>
</record>
```

<br>

아래와 같이 각 공정별 공정 이동표 뷰에서 공통 뷰를 상속받아 `sheet` 안에 `routingx_ids` 필드를 추가했다.

```xml
<record id="lotsheet_lotsheet_routing1_view_form" model="ir.ui.view">
    <field name="name">lotsheet.lotsheet.routing1.form</field>
    <field name="model">lotsheet.lotsheet</field>
    <field name="inherit_id" ref="mrp_ssk.lotsheet_lotsheet_routing_view_form"/>
    <field name="arch" type="xml">
        <xpath expr="//sheet" position="inside">
            <field name="routing1_ids" widget="one2many_lotsheet_limit"
                   context="{'tree_view_ref': 'mrp_ssk.lotsheet_lotsheet_routing1_view_tree_editable', 'form_view_ref': 'mrp_ssk.lotsheet_lotsheet_routing1_view_form_editable',
                             'default_id_workorder': context.get('id_workorder'), 'default_id_staff': context.get('id_staff'), 'default_nu_total_input': context.get('nu_total_input'), 'default_nu_output': context.get('nu_output'),
                             'default_nu_roll_temper': context.get('nu_roll_temper')}"/>
        </xpath>
    </field>
</record>

<record id="lotsheet_lotsheet_routing2_view_form" model="ir.ui.view">
    <field name="name">lotsheet.lotsheet.routing2.form</field>
    <field name="model">lotsheet.lotsheet</field>
    <field name="inherit_id" ref="mrp_ssk.lotsheet_lotsheet_routing_view_form"/>
    <field name="arch" type="xml">
        <xpath expr="//sheet" position="inside">
            <field name="routing2_ids" widget="one2many_lotsheet_limit"
                   context="{'tree_view_ref': 'mrp_ssk.lotsheet_lotsheet_routing2_view_tree_editable', 'form_view_ref': 'mrp_ssk.lotsheet_lotsheet_routing2_view_form_editable',
                             'default_id_workorder': context.get('id_workorder'), 'default_id_staff': context.get('id_staff'), 'default_nu_total_input': context.get('nu_total_input'), 'default_nu_output': context.get('nu_output'),
                             'default_nu_extrusion_temper': context.get('nu_extrusion_temper'), 'default_nu_output_csd': context.get('nu_output_csd'), 'default_lot_csd': context.get('lot_csd')}"/>
        </xpath>
    </field>
</record>
```

<br>

모듈을 업데이트 하고, 검사 공정에서 공정 이동표 뷰를 확인해보니 검사 공정 필드 뿐만 아니라 모든 공정에 필드가 나타났다.

![extension 모드](/no-access-please/assets/image/2022-01-13-odoo-views-inheritance-fields-mode-primary/1.png)

# 해결

뷰를 상속받을 때, mode를 `primary`로 정의해주면 해결된다.

mode는 `extension (default)`과 `primary`, 2가지가 있다. `extension`은 상속한(부모) 뷰가 주체가 되고, `primary`는 상속받은(자식) 뷰가 주체가 된다.

```xml
<field name="mode">primary</field>
```

# 참고

[https://www.odoo.com/documentation/14.0/developer/reference/addons/views.html#inheritance-fields](https://www.odoo.com/documentation/14.0/developer/reference/addons/views.html#inheritance-fields){:target="_blank"}
