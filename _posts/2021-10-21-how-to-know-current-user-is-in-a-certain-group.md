---
layout: post
category: odoo
---

# 문제

사용자가 특정 그룹에 포함되어 있는지 확인하고 싶은 경우가 있다.

나의 경우에는 일반 사용자, 중간 관리자, 최고 관리자 그룹으로 사용자를 구분하고, 그룹에 따라 뷰를 다르게 보여주고 싶은 경우에 사용한다.

# 해결

`has_group` 메소드를 사용해 사용자가 특정 그룹에 포함되어 있는지 확인할 수 있다.

```python
if self.env.user.has_group('base.group_erp_manager'):
    pass
```

# 참고

[https://www.odoo.com/ko_KR/forum/doummal-1/how-to-know-if-the-current-user-is-in-a-certain-group-85273](https://www.odoo.com/ko_KR/forum/doummal-1/how-to-know-if-the-current-user-is-in-a-certain-group-85273){:target="_blank"}