---
layout: post
category: odoo
---

# 문제

Odoo에서 돈에 대한 데이터를 입력할 때는 `Integer`타입이 아닌 `Monetary`타입을 사용한다.

```python
class Book(models.Model):
    _name = 'book.order'

    retail_price = fields.Monetary(string='Retail Price')
```

<br>

책 가격 데이터를 저장하기 위해 `Monetary` 타입의 `retail_price` 필드를 선언했는데, 아래와 같이 오류가 발생했다.

```text
AssertionError: Field book.order.retail_price with unknown currency_field None
```

# 해결

`Monetary` 타입의 필드를 선언하기 위해서는 **통화**를 나타내는 `res.currency` 필드가 필요하다.

```python
class Book(models.Model):
    _name = 'book.order'
    
    currency_id = fields.Many2one('res.currency', string='Currency')
    retail_price = fields.Monetary(string='Retail Price')
```

<br>

통화(currency)에 따라서 화폐(monetary)가 변경된다.

![currency 필드와 Monetary](/no-access-please/assets/image/2021-09-17-odoo-unknown-currency-field-currency-id/1.jpg)

## TMI

한 테이블에서 여러 통화를 사용해야 하는 경우, Monetary 필드를 선언할 때 사용할 통화를 지정한다.

```python
class Book(models.Model):
    _name = 'book.order'

    currency_id = fields.Many2one('res.currency', string='Currency')
    retail_price = fields.Monetary(string='Retail Price', currency_field='currency_id')
```

# 참고

[https://stackoverflow.com/questions/39207876/odoo-unknown-currency-field-currency-id](https://stackoverflow.com/questions/39207876/odoo-unknown-currency-field-currency-id){:target="_blank"}

[https://subscription.packtpub.com/book/programming/9781800200319/4/ch04lvl1sec33/adding-a-monetary-field-to-a-model](https://subscription.packtpub.com/book/programming/9781800200319/4/ch04lvl1sec33/adding-a-monetary-field-to-a-model){:target="_blank"}