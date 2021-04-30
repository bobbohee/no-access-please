---
layout: post
category: odoo 
---

# 문제

파라미터를 설정해 브라우저 파일 캐시 관리를 하려고 했다. 
초기에 파라미터 값으로 현재 시간을 설정해 새로고침을 할 때마다 새롭게 파일이 로드되어, 불필요하게 파일 로드가 일어났다.

파라미터로 현재 시간을 주지 않고, 버전을 설정해 버전을 통해 변경하기로 했다.
모든 파일에 같은 버전을 세팅해주어야하기 때문에 버전을 담고있을 전역 변수가 필요했다.

# 해결

Odoo에 설정(환경 변수)를 저장하는 `ir_config_parameter` 테이블이 따로 존재했다. 
`ir_config_parameter` 테이블에 버전을 저장해 사용했다.

아래 2가지 방법 중 1가지 방법을 택해 사용하면 된다.

# in Odoo Python

```python
# set
self.env['ir.config_parameter'].sudo().set_param('hy_smartcity.version', '2.1.0')

# get
self.env['ir.config_parameter'].sudo().get_param('hy_smartcity.version')
```

# in Odoo Data 

```xml
<?xml version="1.0" encoding="utf-8"?>
<odoo>
    <data noupdate="0">
        <function
            model="ir.config_parameter"
            name="set_param"
            eval="('hy_smartcity.version', '2.1.0')" />
    </data>
</odoo>
```

# 참고

[https://www.odoo.com/ko_KR/forum/doummal-1/is-it-possible-to-define-global-environment-variables-in-odoo-141678](https://www.odoo.com/ko_KR/forum/doummal-1/is-it-possible-to-define-global-environment-variables-in-odoo-141678){:target="_blank"}

[https://www.odoo.com/ko_KR/forum/doummal-1/update-exist-system-parameter-in-ir-config-parameter-xml-153008](https://www.odoo.com/ko_KR/forum/doummal-1/update-exist-system-parameter-in-ir-config-parameter-xml-153008){:target="_blank"}

[https://www.odoo.com/ko_KR/forum/doummal-1/is-there-another-way-to-create-ir-config-parameter-upon-installation-aside-from-xml-153356](https://www.odoo.com/ko_KR/forum/doummal-1/is-there-another-way-to-create-ir-config-parameter-upon-installation-aside-from-xml-153356){:target="_blank"}
