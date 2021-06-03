---
layout: post
category: odoo 
---

# 문제

기존에 차량 예약 데모 데이터를 아래와 같이 생성했었다.

문제는 예약 날짜가 고정되어 있어서, 데모 데이터가 추후에 다시 필요할 때 예약 날짜가 지났다면 예약 날짜를 다시 이후 날짜로 수정해주어야 했었다.

에디터에 replace 기능으로 한 번에 예약 날짜를 바꿀 수 있었지만, 번거로워서 다른 방법을 찾기로 했다.

```xml
<odoo>
    <data noupdate="1">
        <record model="taxi.reservation" id="reservation_1">
            <field name="name">봉브레드</field>
            <field name="address">강원 속초시 동해대로 4344-1</field>
            <field name="reservation_date">2020-05-25 11:30:00</field>
        </record>
    </data>
</odoo>
```

# 해결 

Python에 `datetime` 모듈을 이용하는 방식으로 변경했다.

```xml
<odoo>
    <data noupdate="1">
        <record model="taxi.reservation" id="reservation_1">
            <field name="name">봉브레드</field>
            <field name="address">강원 속초시 동해대로 4344-1</field>
            <field name="reservation_date" eval="(datetime.now().replace(hour=11, minute=0) + timedelta(days=2)).strftime('%Y-%m-%d %H:%M:%S')"/>
        </record>
    </data>
</odoo>
```