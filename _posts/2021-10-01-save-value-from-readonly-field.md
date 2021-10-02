---
layout: post
category: odoo
---

[Set Default Value For One2many Field](/no-access-please/set-default-value-for-one2many-field){:target="_blank"}

# 문제

위 링크처럼 4M 코드 (One2many 필드)에 default 값을 미리 설정해놓고, 수량만 변경이 가능하도록 했다.
근데 저장 버튼을 클릭하니 required로 설정한 `four_m_id` 값이 없다며 오류가 발생했다.
`four_m_id`는 내가 default로 값을 설정해서 없을 수가 없는데...

<br>

create에서 디버깅을 걸어서 확인해보기로 했다.

```python
class LotsheetRouuting54m(models.Model):
    _name = 'lotsheet.routing5.4m'
    _description = 'Inspection Routing 4M'

    routing_id = fields.Many2one('lotsheet.routing5', string='Routing', required=True)
    four_m_id = fields.Many2one('mrp.workcenter.productivity.loss', string='4M Code', required=True)
    four_m_desc = fields.Char(related='four_m_id.four_m_desc', string='4M Description')
    four_m_qty = fields.Integer(string='4M Quantity (EA)', default=0)

    @api.model
    def create(self, vals):
        return super(LotsheetRouuting54m, self).create(vals)
```

<br>

디버깅 결과, `four_m_id` 값이 없었다.

```text
vals = {
    'routing_id': 17,
    'four_m_qty': 20,
}
```

# 해결

default로 설정해둔 4M 코드를 수정하지 못하게 하기 위해 readonly 옵션을 주었는데, Odoo에서 readonly 필드는 저장하지 않는다.

어떻게 생각해보면 당연한 것일수도 있다. 사용자가 값을 입력하지 못하는데...

하지만 나와 같은 상황을 위해 `force_save` 옵션을 사용해 readonly를 설정한 필드를 저장할 수 있다.

```xml
<field name="four_m_ids">
    <tree editable="bottom" create="0" delete="0">
        <field name="four_m_id" readonly="1" force_save="1"/>
        <field name="four_m_desc" readonly="1"/>
        <field name="four_m_qty"/>
    </tree>
</field>
```

<br>

force_save 옵션을 사용하고 이전과 같이 디버깅을 해보니 four_m_id 값이 들어온 것을 확인할 수 있었다.

```text
vals = {
    'routing_id': 17,
    'four_m_id': 2,
    'four_m_qty': 20,
}
```


# 참고

[https://stackoverflow.com/questions/50930525/save-value-from-readonly-field-in-odoo](https://stackoverflow.com/questions/50930525/save-value-from-readonly-field-in-odoo){:target="_blank"}