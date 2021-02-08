---
layout: post
category: openlayers
---

# 문제 

좌표계를 `EPSG:5179`에서 `EPSG:4326`으로 변경하려고 하는데 openlayers 내부에서 아래와 오류가 발생했다.

```text
Uncaught TypeError: Cannot read property 'getCode' of null
```

```javascript
const center = _t.openLayers.getCenter();
const EPSG_5179 = 'EPSG:5179';
const EPSG_4326 = 'EPSG:4326';

const [lon, lat] = ol.proj.transform(center, EPSG_5179, EPSG_4326); // ERROR!
```

# 원인

openlayers에서 `EPSG:5179` 좌표계를 가지고 있지 않았다. 

# 해결

## 좌표계 확인

먼저, openlayers에서 해당 좌표계를 가지고 있는지 확인한다.

해당 좌표계를 가지고 있지 않다면 `null`을 반환한다.

```javascript
ol.proj.get(EPSG_5179);
```

## 좌표계 등록

좌표계를 가지고 있지 않다면, 직접 좌표계 정보를 등록한다.

`proj4.defs()`를 사용하기 위해서는 `proj4js` 라이브러리를 추가해야 한다. 

```javascript
const EPSG_5179_defs = `+proj=tmerc +lat_0=38 +lon_0=127.5 +k=0.9996 +x_0=1000000 +y_0=2000000 +ellps=GRS80 +units=m +no_defs`;
proj4.defs('EPSG:5179', EPSG_5179_defs);
ol.proj.proj4.register(proj4);
```

## 좌표계 변환

좌표 예시 (경기도 시흥시)
- `EPSG:5179` [933360.840286322, 1927035.409445623]
- `EPSG:4326` [126.74768728, 37.33994862]

```javascript
const coordinate = [933360.840286322, 1927035.409445623];

// ol.proj.transform(변환할 좌표, 기존 좌표계, 변환할 좌표계)
const [lon, lat] = ol.proj.transform(center, 'EPSG:5179', 'EPSG:4326');
```

# 참고 사이트
[https://www.python2.net/questions-268595.htm](https://www.python2.net/questions-268595.htm){:target="_blank"}