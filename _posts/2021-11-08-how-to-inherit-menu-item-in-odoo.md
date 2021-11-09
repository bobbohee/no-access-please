---
layout: post
category: odoo
---

# 문제

`base.group_partner_manager` 그룹에 포함된 사용자만 연락처 앱을 볼 수 있도록 하고 싶었다.

그래서 기존에 연락처 앱 menuitem을 상속받아, 아래와 같이 작성하니 데이터베이스에 적용이 되지 않았다.

```xml
<menuitem id="contacts.menu_contacts"
          groups="base.group_partner_manager"/>
```

# 해결

메뉴를 정의할 때, `<menuitem />` 태그를 사용하지만, 이는 `ir.ui.menu` 테이블에 저장되는데 여기서 `res.groups`에 대한 many2many 관계가 정의된다.

`groups_id`에 관계를 업데이트 하기 위해 아래와 같이 작성하면 데이터베이스에 관계가 업데이트 된다.


```xml
<record id="contacts.menu_contacts" model="ir.ui.menu">
    <field name="groups_id" eval="[(6, 0, [ref('base.group_partner_manager')])]"/>
</record>
```

# 참고

[https://www.odoo.com/ko_KR/forum/doummal-1/how-to-inherit-or-override-a-menu-item-67689](https://www.odoo.com/ko_KR/forum/doummal-1/how-to-inherit-or-override-a-menu-item-67689){:target="_blank"}
