---
layout: post
category: odoo 
---

# 문제

기존의 view를 상속받아 `field`나 `button` 등, 재정의할 요소를 가져오기 위해 대부분 `tagname`과 `name` 속성을 사용한다. 

(`field` 태그에서 `name`은 테이블에 정의한 필드명을 가리키고, `button` 태그에서 `name`은 해당 button을 클릭했을 때 실행할 함수를 가리킨다.)

<br>

문제는 간혹 button의 name 속성이 `%()d`로 이루어져있는 경우가 있다. 

```xml
<button type="action" name="%(action_product_replenish)d"/>
```

해당 button을 재정의하기 위해 아래와 같이 작성하면 오류가 난다. 

```xml
<xpath expr="//button[@name='%(action_product_replenish)d']"></xpath>
```

# 해결

`button`의 `name`은 해당 button을 클릭했을 때 실행할 함수를 가리킨다고 했는데 재정의하는 모듈에서 함수를 찾을 수 없기 떄문에 오류가 발생한다.

어떤 모듈의 함수인지를 알 수 있도록 `%(module_name.function_name)d`형식으로 작성해야한다.

```xml
<xpath expr="//button[@name='%(stock.action_product_replenish)d']"></xpath>
```

# 참고

[https://www.odoo.com/fr_FR/forum/aide-1/xpath-how-to-replace-a-window-action-in-odoo-115424](https://www.odoo.com/fr_FR/forum/aide-1/xpath-how-to-replace-a-window-action-in-odoo-115424){:target="_blank"}
