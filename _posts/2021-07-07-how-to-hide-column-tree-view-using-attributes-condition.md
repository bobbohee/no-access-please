---
layout: post
category: odoo
---

# 문제

one2many인 필드에서 기존 조건에 따라 column을 숨기기 위해 `attrs`에 `invisible`을 사용했다.
하지만 숨겨지지 않고, 계속 나타났다. 🤔...

```xml
<field name="lot_names" attrs="{'invisible': [('state', '=', 'done')]}"/>
```

<br>

문제 확인을 위해 `attrs` 속성이 아닌 `invisible` 속성을 사용하니 숨겨졌다. 😨...

```xml
<field name="lot_names" invisible="1"/>
```

# 해결

알고보니, one2many 필드에서는 `attrs`에 `invisible`이 column을 숨기는 것이 아닌 내용을 숨기는 것으로 동작했다. 
one2many 필드는 tree 뷰 형식으로 여러 레코드를 가지고 있어 레코드에 따라 조건이 참일 수도, 거짓일 수도 있기 때문이다.

조건에 따라 column을 숨기고 싶다면 `attrs`에 `column_invisible`을 사용할 수 있다. 
여기서 조건은 one2many 필드를 가지고 있는 부모 테이블이어야 한다.

```xml
<field name="lot_names" attrs="{'column_invisible': [('parent.is_done', '=', True)]}"/>
```


# 참고

[https://www.odoo.com/es_ES/forum/ayuda-1/how-to-hide-column-tree-view-using-attributes-condition-156212](https://www.odoo.com/es_ES/forum/ayuda-1/how-to-hide-column-tree-view-using-attributes-condition-156212){:target="_blank"}
