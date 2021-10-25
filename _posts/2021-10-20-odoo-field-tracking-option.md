---
layout: post
category: odoo
---

# 문제

odoo 뷰에서 특정 필드의 값을 변경하면 값을 변경한 사람과 변경한 시간, 변경한 내용이 기록되어 오른쪽 사이드에 표시된다.

![tracking 옵션 사용 예시](/no-access-please/assets/image/2021-10-20-odoo-field-tracking-option/1.png)

하지만 모든 필드가 변경되었다고 기록되지는 않는다.

고객 관계 관리에 예상 매출이라는 필드를 추가했고, 누군가 예상 매출 값을 변경할 시, 기록을 남기고 싶었다.

# 해결

필드의 값이 변경되었을 때, 기록을 남기기 위해서는 `tracking` 옵션을 활성화해주면 된다.

```python
expected_sales = fields.Monetary(currency_field='company_currency', tracking=True)
```