---
layout: post
category: odoo
---

# 문제

odoo에서 연락처(파트너)의 사업자등록번호가 중복되지 않도록 하기 위해 `unique` 제약 조건을 추가했다.

```python
class ResPartner(models.Model):
    _inherit = 'res.partner'

    _sql_constraints = [
        ('vat_uniq', 'unique (vat)', 'The company vat must be unique !'),
    ]
```

<br>

모듈 업데이트를 진행하니, 아래와 같이 `res.partner` 테이블에 `unique` 제약 조건을 추가할 수 없다는 Log 메세지가 나타났다.

```text
2022-01-07 07:47:14,544 18418 ERROR ent14_ssk_stm_v5 odoo.schema: Table 'res_partner': unable to add constraint 'res_partner_vat_uniq' as unique (vat)
```

# 해결

테이블에 중복된 사업자등록번호가 있어 `unique` 제약 조건을 추가할 수 없는 것이었다.
그래서 아래 SQL query문을 사용해 중복된 사업자등록번호를 조회해 중복되는 사업자등록번호들을 변경했다.

다시 모듈 업데이트를 진행하니 `unique` 제약 조건이 잘 추가되었다.

```sql
select vat, count(vat) from res_partner group by vat having count(vat) > 1;
```

![중복된 사업자등록번호 조회](/no-access-please/assets/image/2022-01-07-sql-unable-to-add-constraint-as-unique/1.png)

# 참고

[https://stackoverflow.com/questions/52658072/sql-server-unable-to-add-constraint](https://stackoverflow.com/questions/52658072/sql-server-unable-to-add-constraint){:target="_blank"}
