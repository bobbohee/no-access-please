---
layout: post
category: odoo
---

# 문제

![공정이동표 4M](/no-access-please/assets/image/2021-10-06-cautions-in-use-required-option-of many2one/1.png)

다른 공정 이동표와 달리 사상 공정과 검사 공정은 4M 수량 입력이 필요했다.

4M 수량을 담는 모델을 따로 두고, 4M 모델에서 공정이동표 ID를 가지고 있어 공정이동표 모델에서는 One2many로 4M 모델을 가져올 수 있도록 했다.

```python
class LotsheetRouting8(models.Model):
    _name = 'lotsheet.routing8'
    _description = 'Inspection Routing'

    four_m_ids = fields.One2many('lotsheet.routing.4m', 'routing_id', string='4M')


class LotsheetRouting84m(models.Model):
    _name = 'lotsheet.routing8.4m'
    _description = 'Inspection Routing 4M'

    routing_id = fields.Many2one('lotsheet.routing', string='Inspection Routing', required=True)
    four_m_id = fields.Many2one('mrp.workcenter.productivity.loss', string='4M Code', required=True)
    four_m_desc = fields.Char(related='four_m_id.four_m_desc', string='4M Description')
    four_m_qty = fields.Integer(string='4M Quantity (EA)', default=0)
```

<br>

4M 코드가 있는 사상 공정과 검사 공정이동표 삭제 시, 아래와 같이 오류가 발생했다.

![레코드 삭제 시 오류 메세지](/no-access-please/assets/image/2021-10-06-cautions-in-use-required-option-of many2one/2.png)

```text
2021-10-06 02:09:43,697 51807 ERROR ent14_ssk_1004 odoo.sql_db: bad query: DELETE FROM lotsheet_routing8 WHERE id IN (4)
ERROR: update or delete on table "lotsheet_routing8" violates foreign key constraint "lotsheet_routing8_4m_routing_id_fkey" on table "lotsheet_routing8_4m"
DETAIL:  Key (id)=(4) is still referenced from table "lotsheet_routing8_4m".

2021-10-06 02:09:43,703 51807 WARNING ent14_ssk_1004 odoo.http: 작업을 완료할 수 있습니다 :다른 모델에서는 레코드를 삭제해야 합니다. 가능하면 대신 보관하십시오.
```

# 해결

`lotsheet.routing8.4m` 모델에 `routing_id`를 `required=True`로 설정한 것이 문제였다.

검사 공정이동표(`lotsheet.routing8`)를 삭제하면, 검사 공정이동표를 Many2one으로 연결한 `lotsheet.routing8.4m`모델에 `routing_id`의 값은 null 값이 된다.
`required=True`로 설정해 null 값을 허용하지 않는데 null 값이 입력되어 오류가 발생한 것이었다.

<br>

검사 공정이동표가 삭제되면 연결된 4M 코드도 같이 삭제되도록 `ondelete='cascade'` 옵션을 주어 해결했다.

```python
routing_id = fields.Many2one('lotsheet.routing', string='Inspection Routing', required=True, ondelete='cascade')
```