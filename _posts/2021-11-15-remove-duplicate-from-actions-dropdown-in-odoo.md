---
layout: post
category: odoo
---

# 문제

오더(`link.order`)의 복제되면 안되는 필드가 많아, 그냥 오더가 복제되지 않기를 원했다.

하지만 기본적으로 조치에 복제와 삭제를 할 수 있는 메뉴가 있기 때문에 복제 메뉴를 누르게 될 가능성이 조금이라도 있어 복제 메뉴를 안 보이게 하고 싶었다.

![조치의 복제 메뉴](/no-access-please/assets/image/2021-11-15-remove-duplicate-from-actions-dropdown-in-odoo/1.png)

# 해결

복제 메뉴를 안 보이게 하기 위해서는 `duplicate` 옵션을 사용하면 된다.

```xml
<form duplicate="0">
    <sheet>
        <group>
            <field name="sale_ids" widget="many2many_links" readonly="1"/>
            <field name="purchase_ids" widget="many2many_links" readonly="1"/>
            <field name="mrp_ids" widget="many2many_links" readonly="1"/>
        </group>
    </sheet>
</form>
```

<br>

하지만, 복제 메뉴가 아니더라도 `copy()` 메소드를 통해 복제될 수 있기 때문에 복제되면 안되는 필드는 copy 옵션을 선언해주어야 했다.

```py
class LinkOrder(models.Model):
    _name = 'link.order'

    sale_ids = fields.Many2many('sale.order', 'link_order_sale_order_rel', 'link_id', 'sale_id', string='Sale Order',
                                copy=False)
    mrp_ids = fields.Many2many('mrp.production', 'link_order_mrp_production_rel', 'link_id', 'mrp_id',
                               string='Production Order', copy=False)
    purchase_ids = fields.Many2many('purchase.order', 'link_order_purchase_order_rel', 'link_id', 'purchase_id',
                                    string='Purchase Order', copy=False)
    # etc...
```

# 참고

[https://www.odoo.com/ko_KR/forum/doummal-1/remove-duplicate-from-actions-dropdown-for-employees-123922](https://www.odoo.com/ko_KR/forum/doummal-1/remove-duplicate-from-actions-dropdown-for-employees-123922){:target="_blank"}
