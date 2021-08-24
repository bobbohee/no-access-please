---
layout: post
category: odoo
---

# 문제

odoo에 상품 테이블에는 `product.template`와 `product.product`이 있는데, 이 두 개의 테이블 차이를 알지 못했다.

# 해결

`product.template`은 상품을 담는 테이블이고, `product.product`은 상품에서 파생된 상품을 담는 테이블이다. 

<br>

`product.template`이 삼성 z플립 3가 있다면, `product.product`에는 삼성 z플립 3 크림 색상, 삼성 z플립 3 그린 색상, ... 이렇게 된다.

<br>

파생 상품이 없는 상품이더라도 `product.template`에 상품을 등록하면 `product.product` 테이블에 상품과 같은 파생 상품이 무조건 생성된다. 

![상품 ERD](/no-access-please/assets/image/2021-08-23-what-is-difference-between-product.product-and-product.template/1.png)

# 참고

[https://stackoverflow.com/questions/50014713/product-and-product-template-in-odoo-10](https://stackoverflow.com/questions/50014713/product-and-product-template-in-odoo-10){:target="_blank"}

[https://www.odoo.com/ko_KR/forum/doummal-1/product-template-vs-product-product-94430](https://www.odoo.com/ko_KR/forum/doummal-1/product-template-vs-product-product-94430){:target="_blank"}
