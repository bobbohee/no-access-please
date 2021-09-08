---
layout: post 
category: odoo
---

# 문제

요구사항에 맞춰 LOT/일련번호가 `일련번호 - 수량` 형식으로 나타나도록 변경했다.

![_rec_name 적용 1](/no-access-please/assets/image/2021-09-08-custom-many2one-widget-list/1.png)

<br>

현재 방식은 `_name_get` 메소드를 사용해 record를 대표하는 이름을 변경한 방식으로, LOT/일련번호 form 뷰에서도 `일련번호 - 수량` 형식으로 나타난다.

![_rec_name 적용 2](/no-access-please/assets/image/2021-09-08-custom-many2one-widget-list/2.png)

```python
class ProductionLot(models.Model):
    _inherit = 'stock.production.lot'

    def name_get(self):
        result = []
        for lot in self:
            name = '%s - %sEA' % (lot.name, str(int(lot.product_qty)))
            result.append((lot.id, name))
        return result
```

<br>

이렇게 적용한 방식은 수량을 함께 보고 싶지 않더라도, 다른 LOT/일련번호 필드를 사용하는 곳에 모두 동일하게 적용되기 때문에 적합한 방식은 아니다.

<br>

또한 이사님께서 일련번호 목록에서만 수량이 보여지고, 아래 사진처럼 선택한 결과에서는 일련번호만 보여져야 한다고 하셔서 현재 방식을 사용할 수 없었다.

![최종 결과](/no-access-please/assets/image/2021-09-08-custom-many2one-widget-list/3.png)

# 해결

## _search 함수 상속

해결할 수 있는 방법은 기존의 many2one 위젯을 custom 위젯을 만드는 방법 뿐이었다.

나타낼 목록을 조회하는 `_search` 함수를 상속받아 재정의했다.

```javascript
odoo.define('sale_management_ssk.field_many2one_lot', function (require) {
    'use strict';

    const FieldRegistry = require('web.field_registry');
    const FieldMany2One = require('web.relational_fields').FieldMany2One;

    const FieldMany2OneLot = FieldMany2One.extend({
        _search: async function (searchValue = "") {
            /* code */
        }
    });

    // custom 위젯 등록
    FieldRegistry.add('many2one_lot', FieldMany2OneLot);

});
```

## 일련번호, 수량 조회

기존 코드를 살펴보면 `name_search` 메소드를 사용해 검색어와 일치하는 레코드의 `name`을 조회한다.

```javascript
const nameSearch = this._rpc({
    model: this.field.relation,
    method: "name_search",
    kwargs: {
        name: value,
        args: domain,
        operator: "ilike",
        limit: this.limit + 1,
        context,
    }
});
```

<br>

우리는 `name_search` 메소드가 아난 `search_read` 메소드를 사용해 검색어와 일치하는 레코드를 찾고, `name`과 `product_qty`를 조회한다.

```javascript
const nameSearch = this._rpc({
    model: this.field.relation,
    method: 'search_read',
    fields: ['name', 'product_qty'],
    domain: [...domain, ['name', 'ilike', value]],
    limit: this.limit + 1,
    context: context,
});
```

## 목록에 나타내기

마지막 return을 보면 `id`, `label`, `value`, `name`으로 객체가 이루어져있다. 
여기서 `label`이 목록에서 보여질 값이므로, `label`에만 `일련번호 - 수량EA` 형식을 적용한다.

```javascript
const nameSearch = this._rpc({
    model: this.field.relation,
    method: 'search_read',
    fields: ['name', 'product_qty'],
    domain: [...domain, ['name', 'ilike', value]],
    limit: this.limit + 1,
    context: context,
});

const results = await this.orderer.add(nameSearch);

// Format results to fit the options dropdown
let values = results.map((result) => {
    const {id, name, product_qty} = result;
    const fullName = `${name} - ${product_qty.toLocaleString()}EA`; // 일련번호 - 수량EA
    const displayName = this._getDisplayName(fullName).trim();
    result[1] = displayName;
    return {
        id,
        label: displayName || data.noDisplayContent, // * 목록에 보여질 값
        value: name,
        name: name,                                                 // * 목록에서 선택 시, 결과로 들어갈 값
    };
});
```