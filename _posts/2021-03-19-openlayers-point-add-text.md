---
layout: post
category: openlayers
---

# 문제

길찾기 경로에는 점과 점(Node)이 있고, 점과 점을 잇는 선(Link)가 있다.
점(Node)에 1부터 순차적으로 텍스트를 표시하고자 했다.

![길찾기 노드 예시](/no-access-please/assets/image/2021-03-19-openlayers-point-add-text/1.png)

# 해결

## 텍스트 정의 (공통)

text는 스타일 속성 내에서 정의할 수 있다.

```javascript
new ol.style.Style({
    text: new ol.style.Text({
        text: '1',
    }),
});
```

이렇게 정의하게 되면 모든 Node가 `1`이라는 텍스트를 표시하게 된다.
나는 순차적으로 (1..2..3..) 표시해야하기 때문에 해당 방법은 사용할 수 없다.

## 텍스트 정의 (개인)

Node 마다 다른 텍스트를 표시하기 위해 `styleFunction` 함수를 통해 `feature` 속성을 가져온다.
`feature`에서 `step`이라는 이름이로 정의한 값을 가져와 `setText` 함수를 사용해 텍스트를 지정한다.

```javascript
const geojson = {
    'type': 'FeatureCollection',
    'crs': {
        'type': 'name',
        'properties': {
            'name': 'EPSG:4326',
        },
    },
    'features': [
        {
            'type': 'Feature',
            'geometry': {
                'type': 'GeometryCollection',
                'geometries': [s_point],
            },
            'properties': {
                'step': '1',
            },
        },
        {
            'type': 'Feature',
            'geometry': {
                'type': 'GeometryCollection',
                'geometries': [s_point],
            },
            'properties': {
                'step': '2',
            },
        }
    ],
};

const style = [
    new ol.style.Style({
        text: new ol.style.Text(),
    }),
];

new ol.layer.Vector({
    source: new ol.source.Vector({
        features: new ol.format.GeoJSON().readFeatures(geojson),
    }),
    style: function styleFunction(feature, resolution) {
        const text = style[0].getText();
        const step = feature.get('step');
        text.setText(step);
        return style;
    },
});
```

# 참고 사이트

[https://openlayers.org/en/latest/examples/vector-labels.html](https://openlayers.org/en/latest/examples/vector-labels.html){:target="_blank"}

[https://geojson.org](https://geojson.org/){:target="_blank"}
