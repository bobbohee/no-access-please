---
layout: post
category: odoo
---

# 문제

오더 주문 데이터를 리스트 뷰로 나타내는데 데이터가 많아질 경우에 대해 처리가 필요했다.
페이지네이션으로 할지 스크롤로 할지 고민하다 빠르게 할 수 있는 스크롤로 처리하기로 했다.

<br>

테이블(`<table>`)에 height를 지정해도 동작하지 않는다.
그래서 테이블에 height를 지정하고 싶은 경우에는 `<table>`를 `<div>`로 감싸고 height를 지정해야 한다.

```html
<div style="height: 200px;">
    <table></table>
</div>
```

<br>

하지만 테이블 전체를 스크롤하게 되면 표의 타이틀(`<thead>`)이 안보이기 때문에 표의 내용(`<tbody>`)만 스크롤되게 하고 싶었다.

# 해결

아래와 같이 스타일을 주면 된다. css를 못해서 어떤 이유로 되는지 까지는 잘 모르겠다... 😅

```css
table tbody {
    display: block;
    max-height: 150px;
    overflow-y: scroll;
}

table thead, table tbody tr {
    display: table;
    width: 100%;
    table-layout: fixed;
}
```

# 참고

[https://stackoverflow.com/questions/23989463/how-to-set-tbody-height-with-overflow-scroll/23989771](https://stackoverflow.com/questions/23989463/how-to-set-tbody-height-with-overflow-scroll/23989771){:target="_blank"}
