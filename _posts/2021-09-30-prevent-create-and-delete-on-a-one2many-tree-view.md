---
layout: post
category: odoo
---

# 문제

odoo에 공정 이동표를 작성할 때, One2many에 4M 코드를 미리 지정해두고 수량만 변경할 수 있도록 했다.

지정한 4M 코드 외에 새로운 4M 코드 추가도, 기존 4M 코드 삭제도 안되게 하기 위해서 `no_create` 옵션을 사용했지만 동작하지 않았다.

# 해결

`no_create`는 Many2one 필드에서 사용하는 속성으로 One2many 필드에는 적용되지 않는다.

One2many 필드에 tree 뷰에서 추가와 삭제를 막기 위해서는 `create` 속성과 `delete` 속성을 사용한다.

```xml
<field name="four_m_ids">
    <tree editable="bottom" create="0" delete="0">
        <field name="four_m_type"/>
        <field name="four_m_qty"/>
    </tree>
</field>
```

# 참고

[https://stackoverflow.com/questions/63071176/prevent-create-and-delete-on-a-one2many-tree-view](https://stackoverflow.com/questions/63071176/prevent-create-and-delete-on-a-one2many-tree-view){:target="_blank"}