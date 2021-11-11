---
layout: post
category: odoo
---

# 문제

공정에서 필요한 설비를 등록할 때, 사용 가능한 다른 설비들을 등록하고자 했다.

A 설비에 등록한 사용 가능한 설비를 B 설비에도 등록할 수 있기 때문에, 카테고리를 구성하는 것처럼 같은 테이블에서 many2one, one2many 관계를 가질 수는 없고, manymany를 사용해야 했다.

<br>

아래와 같이 선언하면 오류가 발생한다.

```python
sub_equipment_ids = fields.Many2many('maintenance.equipment')
```

```text
AssertionError: maintenance.equipment.maintenance_equipments: Implicit/canonical naming of many2many relationship table is not possible when source and destination models are the same
AssertionError: maintenance.장비.maintenment_장비: 소스 모델과 대상 모델이 동일한 경우 many2many 관계 테이블을 암시적/캐논적 이름으로 지정할 수 없습니다.
```

# 해결

오류를 번역기에 돌려서 의미를 해석해보면 같은 테이블에서 many2many 관계를 사용할 경우 odoo에서 many2many 관계 테이블 명을 지정해줄 수 없다는 이야기이다.

odoo에서는 many2many 테이블 명을 따로 선언해주지 않으면 소스 모델과 대상 모델을 가지고 many2many 관계 테이블 명을 자동으로 생성해주는데, 소스 모델과 대상 모델이 같은 모델일 경우에 자동으로 생성해 해줄 수 없으니 테이블 명을 직접 지정해야 한다.

```python
sub_equipment_ids = fields.Many2many('maintenance.equipment', 'maintenance_equipment_main_sub_rel', 'main_id', 'sub_id', string='Sub Equipments')
```
