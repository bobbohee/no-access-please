---
layout: post
category: openlayers
---

# 문제

길찾기 경로 노드 클릭 시, 해당 경로의 이동 방법을 팝업으로 나타내고자 했다.

![길찾기 노드 팝업](/no-access-please/assets/image/2021-03-29-openlayers-feature-get-coordinates-not-working/1.png)

<br>

해당 노드 클릭 시, 팝업을 나타내는 함수에서 `getCoordinates()`함수가 존재하지 않는다는 오류를 출력했다. 

```javascript
feature.getGeometry().getCoordinates();
```

# 원인

마커는 `Geometry` 타입, 노드는 Geojson을 사용해 생성했기 때문에 `GeometryCollection` 타입이었다.

팝업을 나타내는 함수에서 좌표를 가져오기 위해 사용한 아래 코드는 feature가 `Geometry` 타입일 때만 사용 가능하다.

```javascript
feature.getGeometry().getCoordinates();
```

# 해결

feature가 `GeometryCollection` 타입인지 `Geometry` 타입인지를 구분해 좌표를 다르게 가져오는 방법으로 수정했다.

## Geometry 타입

```javascript
feature.getGeometry().getCoordinates();
```

## GeometryCollection 타입

```javascript
const geometry = feature.getGeometry();
const geometries = geometry.getGeometries();

let coordinates = [];

for (const geom of geometries) {
    coordinates = coordinates.concat(geom.getCoordinates());
}
```

## 전체 코드

```javascript
let coordinate;
const geometry = feature.getGeometry();

if (geometry instanceof ol.geom.GeometryCollection) {
    const geometries = geometry.getGeometries();
    let coordinates = [];

    for (const geom of geometries) {
        coordinates = coordinates.concat(geom.getCoordinates());
    }

    coordinate = coordinates;
} else {
    coordinate = feature.getGeometry().getCoordinates();
}

_t.popup.setPosition(coordinate);
```

# 참고

[https://gis.stackexchange.com/questions/249580/get-all-the-coordinates-of-a-feature-in-openlayers-4](https://gis.stackexchange.com/questions/249580/get-all-the-coordinates-of-a-feature-in-openlayers-4){:target="_blank"}
