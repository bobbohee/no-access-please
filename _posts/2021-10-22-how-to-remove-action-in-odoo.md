---
layout: post
category: odoo
---

# 문제

권한에 따라 CRM(고객 관계 관리)에서 예상 수익을 볼 수 없도록 설정했다.
그래프, 피벗, 코호트 뷰에서도 측정 값으로 예상 수익을 볼 수 없도록 설정했는데 이상하게 대쉬보드에서는 나타났다.
대쉬보드는 기존에 있는 그래프, 피벗, 코호트 뷰를 불러와 보여주는 뷰였는데 이상하게 단독으로 있는 뷰에서는 예상 수익이 안보였지만, 대쉬보드로 들어오면 예상 수익이 나타났다.

결국 해결 방법을 찾지 못해, 일단 대시보드를 화면에서 제외하기로 했다.
그러기 위해서는 action과 연결된 대쉬보드 view를 없애야했다.

# 해결

`delete` 태그를 사용해 `model`과 `id` 속성을 정의해 삭제할 view를 정의한다.

```xml
<delete model="ir.actions.act_window.view" id="crm_enterprise.crm_opportunity_action_dashboard_dashboard"/>
```

일반적으로 쓰이는 방법은 아니다. 정말 필요할 때만 사용하도록 하자!

# 참고

[https://www.odoo.com/ko_KR/forum/doummal-1/hide-an-act-window-id-154276](https://www.odoo.com/ko_KR/forum/doummal-1/hide-an-act-window-id-154276){:target="_blank"}