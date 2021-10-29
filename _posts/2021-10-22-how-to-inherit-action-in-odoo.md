---
layout: post
category: odoo
---

# 문제

권한에 따라 CRM(고객 관계 관리)에서 예상 수익을 볼 수 없도록 설정했다.
그래프, 피벗, 코호트 뷰에서도 측정 값으로 예상 수익을 볼 수 없도록 설정했는데 이상하게 대쉬보드에서는 나타났다.
대쉬보드는 기존에 있는 그래프, 피벗, 코호트 뷰를 불러와 보여주는 뷰였는데 이상하게 단독으로 있는 뷰에서는 예상 수익이 안보였지만, 대쉬보드로 들어오면 예상 수익이 나타났다.

결국 해결 방법을 찾지 못해, 일단 대시보드를 화면에서 제외하기로 했다.
그러기 위해서는 action을 상속받아 `view_mode`에서 dashboard를 제거해줘야 했다.

# 해결

action을 상속받아 재정의하는 방법은 view를 상속받아 재정의하는 방법과는 약간 다르다.

<br/>

view는 `inherit_id`를 통해 상속받을 뷰를 가져온다.

```xml
<record id="enterprise_crm_lead_view_pivot" model="ir.ui.view">
    <field name="name">crm.lead.pivot.view.inherit.crm_tilon</field>
    <field name="model">crm.lead</field>
    <field name="inherit_id" ref="crm_enterprise.crm_lead_view_pivot"/>
    <field name="arch" type="xml">
        <!-- 재정의 코드 작성 ... -->
    </field>
</record>
```

<br/>

하지만 action은 `id`에 상속받을 action을 적어준다.

```xml
<record id="crm_enterprise.crm_opportunity_action_dashboard" model="ir.actions.act_window">
    <field name="view_mode">graph,pivot,tree,form,cohort</field>
</record>
```

# 참고

[https://www.odoo.com/ko_KR/forum/doummal-1/how-can-i-inherit-action-14729](https://www.odoo.com/ko_KR/forum/doummal-1/how-can-i-inherit-action-14729){:target="_blank"}