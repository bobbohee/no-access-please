---
layout: post
category: openlayers
---

# 문제

경로 마다 이동성 정보를 반영한 색상으로 표현하고자 했다.

![길찾기 경로 다중 스타일](/no-access-please/assets/image/2021-03-22-openlayers-feature-set-style/1.png)

<br>

기존 방법은 layer에 style을 적용했다. 
layer에 style을 적용했을 떄, layer에 feature는 동일한 style을 가지게 된다.

# 해결

layer에 style을 적용하는 것이 아닌, feature에 style을 적용해야 한다.

## setStyle

```javascript
const layer = new ol.layer.Vector({
    source: new ol.source.Vector({
        features: new ol.format.GeoJSON().readFeatures(geojson),
    }),
});

layer.setStyle((feature) => {
    return new ol.style.Style({
        stroke: new ol.style.Stroke({
            color: '#cc2900', // feature 별 color 지정
            width: 8,
        }),
    });
});
```

## style function

```javascript
const layer = new ol.layer.Vector({
    source: new ol.source.Vector({
        features: new ol.format.GeoJSON().readFeatures(geojson),
    }),
    style: function (feature, resolution) {
        return new ol.style.Style({
            stroke: new ol.style.Stroke({
                color: '#cc2900', // feature 별 color 지정
                width: 8,
            }),
        });
    },
});
```

# 참고

[https://gis.stackexchange.com/questions/164984/openlayers-3-extracting-data-for-styling-from-my-geojson](https://gis.stackexchange.com/questions/164984/openlayers-3-extracting-data-for-styling-from-my-geojson){:target="_blank"}

[https://openlayers.org/en/latest/apidoc/module-ol_style_Style-Style.html](https://openlayers.org/en/latest/apidoc/module-ol_style_Style-Style.html){:target="_blank"}
