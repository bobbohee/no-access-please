---
layout: post
category: odoo
---

# 문제

odoo에서 공정 이동표를 작성할 때 필요한 4M 코드가 공정 이동표 별로 변경되지 않고, 고정되어 있어 One2many로 연결된 4M 코드를 미리 지정해두고 수량만 변경할 수 있도록 하고 싶었다.

![SSK 4M 코드](/no-access-please/assets/image/2021-09-30-set-default-value-for-one2many-field/1.png)

(예시)

![One2many 4M 코드 적용 예시](/no-access-please/assets/image/2021-09-30-set-default-value-for-one2many-field/2.png)

# 해결

odoo에서 그런 기능을 제공할까 싶었지만, 다행히 제공하고 있었다.

설정 -> 기술 -> 자원 -> 근무 시간을 보면 내가 원하는 기능인 One2many 필드에 default 값을 주는 것이 가능하다는 것을 알 수 있다.

```python
@api.model
def default_get(self, fields_list):
   res = super(classname, self).default_get(fields_list)
   vals = [(0, 0, {'field_1': value_1, 'field_2': value_2}),
           (0, 0, {'field_1': value_1, 'field_2': value_2})]
   res.update({'your_o2m_field': vals})
   return res
```

<br>

data.xml에 미리 정의해둔 4M 코드를 불러오고, 수량은 0으로 초기화 해준다.

```python
@api.model
def default_get(self, fields_list):
   res = super(LotsheetRouting3, self).default_get(fields_list)
   vals = [(0, 0, {'four_m_id': self.env.ref('mrp_ssk.four_m_MT01').id, 'four_m_qty': 0}),
           (0, 0, {'four_m_id': self.env.ref('mrp_ssk.four_m_MA01').id, 'four_m_qty': 0})]
   res.update({'four_m_ids': vals})
   return res
```

# 참고

[https://www.odoo.com/forum/help-1/set-default-value-for-one-of-the-one2many-field-odoo-11-149093](https://www.odoo.com/forum/help-1/set-default-value-for-one-of-the-one2many-field-odoo-11-149093){:target="_blank"}