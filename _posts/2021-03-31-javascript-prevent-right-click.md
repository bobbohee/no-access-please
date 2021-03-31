---
layout: post
category: javascript 
---

# 문제

브라우저에서 우클릭 시, 나타나는 메뉴를 `contextmenu`라고 한다.

<img src="/no-access-please/assets/image/2021-03-31-javascript-prevent-right-click/1.png" alt="contextmenu" width="50%"/>

<br>

우클릭 시, 나타나는 메뉴를 막는 방법은 두 가지가 있다. 
여기서 1번 방법을 사용했는데 우클릭 시 메뉴가 그대로 나타났다. 

```javascript
document.addEventListener('contextmenu', (e) => {
    return false;
});
```

```html
<body oncontextmenu="return false"></body>
```

# 해결

`return false`가 아닌 `e.preventDefault()`를 사용해 우클릭 창 동작을 막는다.

```javascript
document.addEventListener('contextmenu', (e) => {
    e.preventDefault();
});
```

<br>

👉 [contextmenu 커스텀](https://codepen.io/tobiasdev/pen/LRaBaX){:target="_blank"}

# 참고

[https://codinhood.com/nano/dom/disable-context-menu-right-click-javascript](https://codinhood.com/nano/dom/disable-context-menu-right-click-javascript){:target="_blank"}