---
layout: post
category: javascript
---

# 문제

Odoo에서 `판매 - 오더`, `오더 - 구매`, `오더 - 제조` 연결하는 기능을 개발하기 전에 어떻게 코드를 작성할지 고민했다.
요구사항이 비슷했기 때문에 중복되는 기능을 하나의 클래스에 정의하고 각 모듈에서 상속받아 재정의하거나 확장해 사용하기로 했다.

<br>

연결 여부를 판단하는 필드는 각각 달라 상속받아 연결 여부를 판단하는 필드를 선언해주었다.

```javascript
const LinkSaleModel = LinkOrderModel.extend({
    init: function (parent, params) {
        this.linkField = 'link_id';
        this._super.apply(this, arguments)
    },
});
```

<br>

연결 여부를 체크함 / 체크하지 않음에 따라 데이터베이스에 연결 여부를 저장해야했고, 연결 여부를 판단하는 필드를 담은 `linkField` 변수를 object의 key로 사용하고 싶었다.

아래와 같이 \``${this.linkField}`\` 와 같이 쓰면 된다고 생각했지만, 아니었다.

```javascript
setIsLink: function (id = 0, value = undefined) {
    if (id && value !== undefined) {
        return this._rpc({
            model: 'sale.order.line',
            method: 'write',
            args: [id, {
                `${this.linkField}`: value,
            }],
        });
    }
},
```

# 해결

object의 key 값으로 template string (\`\`)을 사용하고 싶은 경우에는, 대괄호([])로 감싸주어야 한다.

```javascript
setIsLink: function (id = 0, value = undefined) {
    if (id && value !== undefined) {
        return this._rpc({
            model: 'sale.order.line',
            method: 'write',
            args: [id, {
                [`${this.linkField}`]: value,
            }],
        });
    }
},
```

# 참고

[https://stackoverflow.com/questions/33194138/template-string-as-object-property-name](https://stackoverflow.com/questions/33194138/template-string-as-object-property-name){:target="_blank"}