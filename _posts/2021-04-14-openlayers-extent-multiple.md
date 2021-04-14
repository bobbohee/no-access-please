---
layout: post
category: openlayers 
---

# 문제

마커를 생성하거나 경로를 나타내었을 때, 화면에 맞게 줌과 센터를 조정하고 싶었다.
`getExtent()` 메서드를 통해 feature 범위를 가져오고, `fit()` 메서드를 통해 범위에 맞게 줌과 센터를 조정할 수 있다. 

문제는 경로를 나타낼 때 노드 레이어와 링크레이어, 마커 레이어가 따로 있기 때문에 1개(특정) 레이어의 feature 범위가 아닌, 여러 개 레이어의 feature 범위를 구하고 싶었다.

# 해결

## 특정 레이어

```javascript
const extent = layer.getSource().getExtent();

map.getView().fit(extent);
```

## 여러 레이어

```javascript
const extent = ol.extent.createEmpty();

for (const layer of layers) {
    ol.extent.extend(extent, layer.getSource().getExtent());
}

map.getView().fit(extent);
```

# 참고

[https://stackoverflow.com/questions/30121024/openlayers-3-zoom-to-combined-extent](https://stackoverflow.com/questions/30121024/openlayers-3-zoom-to-combined-extent){:target="_blank"}