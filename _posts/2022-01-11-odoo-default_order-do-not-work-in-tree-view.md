---
layout: post
category: odoo
---

# 문제

제조 주문서를 작업 진행 순서대로 정렬하기 위해 `default_order` 속성을 사용해 `workcenter_code`를 기준으로 오름차순으로 정렬하도록 했다.

하지만 오름차순으로 정렬되지 않았고, `default_order` 속성 대신 모델에 `_order` 속성을 사용해도 정렬이 되지 않았다.

```xml
<tree string="Manufacturing Orders" default_order="workcenter_code asc">
    <!-- code -->
</tree>
```

![default_order 속성 사용](/no-access-please/assets/image/2022-01-11-odoo-default_order-do-not-work-in-tree-view/1.png)


# 해결

알고보니, 제조 주문서 페이지에 적용되어 있던 기본 즐겨찾기 때문이었다.
이 즐겨찾기를 아예 제거하고, 페이지를 새로 고침해보니 `workcenter_code`를 기준으로 오름차순 정렬되었다.

![제조 주문서 즐겨찾기](/no-access-please/assets/image/2022-01-11-odoo-default_order-do-not-work-in-tree-view/2.png)

<br>

더 정확한 원인을 알아보기 위해 즐겨찾기 테이블(`ir.filters`)을 살펴보니 즐겨찾기를 저장할 때 현재 정렬 기준(`sort`)까지 함께 저장이 되어, `default_order` 속성이 동작하지 않은 것이었다.



| id | name     | domain  | context                       | sort                                        | model_id       | id_default |
|:---|:---------|:--------|:------------------------------|:--------------------------------------------|:---------------|:-----------|
| 15 | 제조 주문서 | []      | {'group_by': ['order_group']} | ["priority desc","date_planned_start desc"] | mrp.production | true       |


# 참고

[https://www.odoo.com/documentation/14.0/developer/reference/addons/views.html?highlight=default_order#list](https://www.odoo.com/documentation/14.0/developer/reference/addons/views.html?highlight=default_order#list)
