---
layout: post
category: odoo
---

# 문제

product.template에서 품질관리점을 설정하면 product.product와 quality.point(품질관리점) 간의 Many2Many 관계를 설정해야 했다.
그러기 위해서는 계산해서 필드의 값 넣는 `compute` 옵션을 사용해야했다. 
 
many2many 필드에는 `compute`를 사용할 수 없을 거라고 생각했는데, 코드를 검색해보니 `compute`를 사용한 코드가 있어서 아래와 같이 코드를 작성하고 테스트를 위해 디버그를 걸었는데 이상하게 디버그에 걸리지 않았다.

```python
quality_point_ids = fields.Many2many('quality.point', string='Quality Point', compute='_compute_quality_point_ids')

@api.depends('product_tmpl_id.quality_point_id')
def _compute_quality_point_ids(self):
    for product in self:
        quality_point_id = product.product_tmpl_id.quality_point_id.id
        product.quality_point_ids = [(6, 0, [quality_point_id])]
```

잘못된 문법을 작성했나 싶어 확인해봤지만 아니었고, many2many에서는 안되나 싶어 many2many가 아닌 다른 자료형(Char)으로 해보니 디버그에 걸렸다. 

# 해결

`store=True` 옵션을 적어주면 된다. store 옵션은 계산된 값을 DB에 저장할 지에 대한 여부인데 기능에 따라 자유롭게 사용할 수 있다.

근데 Many2many 필드에서는 `True`로 주어야만 compute 메소드가 호출된다. 

(왜 그런건지 정확한 이유는 모르겠지만...)

```python
quality_point_ids = fields.Many2many('quality.point', string='Quality Point', 
                                      compute='_compute_quality_point_ids', store=True)

@api.depends('product_tmpl_id.quality_point_id')
def _compute_quality_point_ids(self):
    for product in self:
        quality_point_id = product.product_tmpl_id.quality_point_id.id
        product.quality_point_ids = [(6, 0, [quality_point_id])]
```
