---
layout: post
category: odoo
---

# 문제

javascript에서 필드 값을 변경하고, 강제로 onchange 함수를 호출하기 위해 javascript에서 python 함수를 호출하고 싶은 경우가 있었다.

# 해결

javascript에 `_rpc` 메소드를 사용해 python 함수를 호출할 수 있다.

- `model`: 함수를 선언한 model 명

- `method`: 함수명

- `args`: 함수 인자값

    ⚠️ 첫 번째 인자로 mrp.production 모델의 id 값을 넘겨주어야 `self`를 사용할 수 있다.

```javascript
setProductQty: function (product_qty) {
    return this._rpc({
        model: 'mrp.production',
        method: 'set_product_qty',
        args: [[this.activeId], product_qty]
    });
}
```

```python
class MrpProduction(models.Model):
    _inherit = 'mrp.production'

    def set_product_qty(self, product_qty):
        """ Forced method call related to the product_qty field """
        self.product_qty = product_qty
        self._onchange_product_qty()
        self._onchange_move_raw()
        self._onchange_move_finished()
```

# 참고

[https://www.odoo.com/forum/help-1/call-python-function-from-javascript-in-odoo12-142822](https://www.odoo.com/forum/help-1/call-python-function-from-javascript-in-odoo12-142822){:target="_blank"}
