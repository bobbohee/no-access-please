---
layout: post
category: openlayers
---

# 문제

브라우저에서 우클릭 시, 나타나는 메뉴를 `contextmenu`라고 한다.

<img src="/no-access-please/assets/image/2021-03-31-openlayers-prevent-right-click/1.png" alt="contextmenu" width="50%"/>

<br>

브라우저 전체가 아닌 openlayers map에서 우클릭 시, contextmenu 창 이벤트를 방지한다.

# 해결

`map.getViewport()`를 통해 map이 있는 dom을 가져와 contextmenu 이벤트를 등록한다.
`e.preventDefault()`로 contextmenu 창이 나타남을 막는다. 

```html
map.getViewport().addEventListener('contextmenu', (e) => {
    event.preventDefault();
});
```

# 참고

[https://stackoverflow.com/questions/41477576/mouse-rightclick-on-openlayer-3](https://stackoverflow.com/questions/41477576/mouse-rightclick-on-openlayer-3){:target="_blank"}