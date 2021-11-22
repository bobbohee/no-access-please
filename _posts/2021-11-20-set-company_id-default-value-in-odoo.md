---
layout: post
category: odoo
---

# 설명

새로운 모델을 추가할 때, 필수는 아니지만 기본적으로 `company_id` 필드를 추가한다.
여러 회사에서 Odoo를 같이 이용하는 경우, 거의 대부분 각자 회사의 데이터를 공유하고 싶지 않기 때문이다.
그래서 `company_id` 필드에 회사를 설정하고, 같은 회사의 데이터만 조회되도록 규칙을 추가한다.

```xml
<record id="maintenance_equipment_comp_rule" model="ir.rule">
    <field name="name">Maintenance Equipment Multi-company rule</field>
    <field name="model_id" ref="model_maintenance_equipment"/>
    <field name="domain_force">['|', ('company_id', '=', False), ('company_id', 'in', company_ids)]</field>
</record>
```

새로 데이터를 작성할 때마다 회사를 선택해주기 번거로워 default로 값을 설정하는데, 잘못된 값을 default로 설정하게 되면 다른 회사의 데이터로 들어가버리기 때문에 주의해야 한다.

# 방법

다양한 방법이 있겠지만, 대부분 아래 2가지 방법을 사용한다.

## 1. 현재 접속(active)된 회사로 설정

![현재 접속(active)된 회사로 설정](/no-access-please/assets/image/2021-11-20-set-company_id-default-value-in-odoo/1.png)

```python
def _get_default_company_id(self):
    return self.env.company.id

company_id = fields.Many2one('res.company', string='Company', required=True, default=_get_default_company_id)
```

## 2. 현재 로그인한 사용자의 기본 회사로 설정

![현재 로그인한 사용자의 기본 회사로 설정](/no-access-please/assets/image/2021-11-20-set-company_id-default-value-in-odoo/2.png)

```python
def _get_default_company_id(self):
    return self.env.user.company_id.id

company_id = fields.Many2one('res.company', string='Company', required=True, default=_get_default_company_id)
```

# 주의할 점

2가지 방법 모두 허용된 회사가 기본 회사 뿐인 사용자는 문제가 되지 않는다. 그러나 허용된 회사가 기본 회사 뿐만 아니라 여러 회사인 사용자(관리자)의 경우 문제가 될 수 있다.

[1] **에스에스아이** 회사로 접속(active)한 사용자의 [2] 기본 회사가 **에스에스케이**인 경우, 아래와 같이 default 값이 다르게 설정된다.

![1번, 2번 예시](/no-access-please/assets/image/2021-11-20-set-company_id-default-value-in-odoo/3.png)

<br>

위 주의할 점을 보고, `company_id` 필드에 의도에 맞는 default 값을 설정해야 한다.