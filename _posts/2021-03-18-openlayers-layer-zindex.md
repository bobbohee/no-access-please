---
layout: post
category: openlayers
---

# 문제 

마커부터 경로가 시작하지 않고, 마커에서 조금 떨어진 위치 (건물 입구 등)에서 경로 탐색이 시작되어 **출발 마커-경로 탐색 시작점, 도착 마커-경로 탐색 종료점**을 이어 경로가 자연스러워 보이게 하고자 했다.

마커와 경로 탐색 링크(파란색)를 잇는 연결 링크(주황색) 레이어가 마커 레이어보다 후에 추가되어 마커를 가리는 문제가 발생했다.

![마커 링크 순서](/no-access-please/assets/image/2021-03-18-openlayers-layer-zindex/1.png)

# 해결

`zIndex` 속성을 사용해 레이어 순서를 조정할 수 있다. (기본 값은 `0`이다.)

음수(-) 값도 사용 가능하지만, 음수 값을 사용하면 지도 레이어가 있을 때 지도 레이어 뒤로 해당 레이어가 숨겨지기 때문에 양수(+) 값을 사용해 순서를 조정하는 것이 좋다.

## 레이어 생성 시, 지정

레이어를 생성할 때 `zIndex` 속성을 지정해 순서를 조정할 수 있다. 

```javascript
const layer = new ol.layer.Vector({
    title: `marker-layer`,
    source: new ol.source.Vector(),
    zIndex: 5,
});
```

## 레이어 생성 후, 지정

어떤 이벤트에 의해 레이어 순서가 조정되어야 된다면 아래처럼 함수를 통해 레이어 순서를 조정할 수 있다.

```javascript
const layer = new ol.layer.Vector({
    title: `marker-layer`,
    source: new ol.source.Vector(),
});

layer.setZIndex(5);
```

# 참고 사이트

[https://openlayers.org/en/latest/examples/layer-z-index.html](https://openlayers.org/en/latest/examples/layer-z-index.html){:target="_blank"}

[https://openlayers.org/en/latest/apidoc/module-ol_layer_BaseTile-BaseTileLayer.html#setZIndex](https://openlayers.org/en/latest/apidoc/module-ol_layer_BaseTile-BaseTileLayer.html#setZIndex){:target="_blank"}