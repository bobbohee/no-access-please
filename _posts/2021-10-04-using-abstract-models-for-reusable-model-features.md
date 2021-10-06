---
layout: post
category: odoo
---

# 문제

공정 이동표 개발을 담당했다. 공정 이동표는 각 공정별로 작업이 끝나고, 공정에 대한 결과물을 기록하는 표 같은 것이다.
작업에 필요한 제품과 수량, 작업을 마친 결과 제품과 수량, 불량 수량, 작업자, 작업 시간 등 여러 정보를 기입하게 되어있었다.

공정별로 입력해야하는 특수한 정보가 있었지만, 작업자, 작업 시간 등 공정별로 동일하게 입력해야하는 공통 정보가 있었다.
공정별로 테이블을 따로 나누어 데이터베이스에 데이터를 저장했는데, 공통적으로 필요한 필드를 테이블마다 선언하니 관리하기가 힘들었다.

공통된 필드를 선언하는 테이블을 하나 생성하고, 공정별 테이블에서 상속받아 특수한 필드만 추가하는 형식으로 개발하기로 했다.

원래라면, 테이블을 생성하고 필드를 작성할 때 `models.Model`을 상속받아 아래와 같이 작성한다.

```python
class Person(models.Model):
    _name = 'person.person'
    _description = 'Common Person'

    name = fields.Char(string='Name')
    age = fields.Integer(string='Age')
    gender = fields.Selection([('female', 'Female'), ('male', 'Male')], string='Gender')
```

이렇게 되면 공통적인 필드를 선언한 `person.person`은 다른 테이블에서 상속을 받기 위해 필요한 테이블이기 떄문에, 테이블이 생성되면 안되지만 생성되는 문제가 있다.

# 해결

이러한 경우를 위해서 `models.AbstractModel`을 사용할 수 있다.

`models.AbstractModel`로 선언된 테이블은 테이블 템플릿을 정의한다는 의미로, 실제로 테이블이 생성되지는 않는다.

```python
class PersonPerson(models.AbstractModel):
    _name = 'person.person'

    name = fields.Char(string='Name')
    age = fields.Integer(string='Age')
    gender = fields.Selection([('female', 'Female'), ('male', 'Male')], string='Gender')


class PersonTeenage(models.Model)
    _name = 'person.teenage'
    _inherit = ['person.person']

    school = fields.Char(string='School Name')
```

<br>

`models.AbstractModel`을 상속받아 선언하는 방법 외에도 옵션을 주는 방법이 있다.

`_auto = False`로 설정하면, 자동으로 테이블이 생성되는 것을 방지한다.

```python
class PersonPerson(models.Model):
    _name = 'person.person'
    _auto = False

    name = fields.Char(string='Name')
    age = fields.Integer(string='Age')
    gender = fields.Selection([('female', 'Female'), ('male', 'Male')], string='Gender')
```

`_abstract = True`로 설정하면, 테이블이 추상적이라는 것을 의미해 테이블이 생성되지 않는다.

```python
class PersonPerson(models.Model):
    _name = 'person.person'
    _abstract = True

    name = fields.Char(string='Name')
    age = fields.Integer(string='Age')
    gender = fields.Selection([('female', 'Female'), ('male', 'Male')], string='Gender')
```

# 참고

[https://www.odoo.com/documentation/14.0/developer/reference/addons/orm.html?highlight=models%20abstractmodel#odoo.models.AbstractModel](https://www.odoo.com/documentation/14.0/developer/reference/addons/orm.html?highlight=models%20abstractmodel#odoo.models.AbstractModel){:target="_blank"}

[https://subscription.packtpub.com/book/programming/9781800200319/4/ch04lvl1sec43/using-abstract-models-for-reusable-model-features](https://subscription.packtpub.com/book/programming/9781800200319/4/ch04lvl1sec43/using-abstract-models-for-reusable-model-features){:target="_blank"}

