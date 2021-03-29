---
layout: post
category: openlayers
---

# 문제

어떠한 이벤트 발생 시, 특정 feature에 fill 색상을 변경하고자 했다.

![길찾기 경로 특정 노드](/no-access-please/assets/image/2021-03-29-openlayers-change-circle-fill-color/1.png)

<br>

색상을 변경하는 함수를 사용했지만 색상이 변경되지 않았다.

```javascript
style.getImage().getFill().setColor('#2E70FB');
```


# 원인

아래 코드와 같이 원 모양으로 나타내기 위해 `new ol.style.Circle`을 사용했는데, Circle에 File 색상 변경 시, feature가 리렌더링이 되어야 하는데 리렌더링이 되지 않는 이슈가 있었다. 

```javascript
new ol.style.Style({
    image: new ol.style.Circle({
        // code ...
    }),
    text: new ol.style.Text({
        // code ...
    }),
});
```

해당 이슈는 openlayers 깃허브 레포지토리에 이미 이슈로 등록되었지만, 댓글에 억지로 리렌더링 방법만 있을뿐 따로 개선되지는 않았다.

👉 [이슈 확인하기](https://github.com/openlayers/openlayers/issues/7398){:target="_blank"}

# 해결

`ol.style.Circle`에 `setRadius()` 함수를 사용해 강제로 리렌더링 하도록 한다.

`setRadius()`를 통해 강제로 리렌더링이 되면서 색상이 변경된다.

```javascript
const image = style.getImage();

image.getFill().setColor('#2E70FB');
// Force circle rendering
image.setRadius(image.getRadius());
```

# 참고

[https://github.com/openlayers/openlayers/issues/7398](https://github.com/openlayers/openlayers/issues/7398){:target="_blank"}