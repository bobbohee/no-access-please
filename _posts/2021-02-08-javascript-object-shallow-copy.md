---
layout: post
category: javascript 
---

# 문제

각각 검색 맵과 길찾기 맵에서 center와 zoom을 변경했을 때, 각 search, route 변수에 값을 담아 활용하고자 했다.

default 변수 값을 기본으로 주었는데 1개의 변수 값이 변경되니 3개 변수가 모두 동일한 값으로 변경되었다.

```javascript
constructor() {
    this.default = {
        center: [931832.6601704739, 1928523.7630699435],
        zoom: 14,
    };
    this.search = this.default;
    this.route = this.default;
}
```

# 원인
Object는 참조값으로 변수에 대입 시, 값을 가르키지 않고 주소를 가르킨다. (깊은 복사)

3개의 변수에 주소가 모두 같아 1개 변수 값이 변경되면 모두 변경되는 것이다. 

# 해결
변수 대입 시, 주소가 값을 가르키도록 한다. (얕은 복사)

## Object.assign()
```javascript
constructor() {
    this.default = {
        center: [931832.6601704739, 1928523.7630699435],
        zoom: 14,
    };
    this.search = Object.assign({}, this.default);
    this.route = Object.assign({}, this.default);
}
```

## 전개연산자
```javascript
constructor() {
    this.default = {
        center: [931832.6601704739, 1928523.7630699435],
        zoom: 14,
    };
    this.search = {...this.default};
    this.route = {...this.default};
}
```

# 참고 사이트
[https://velog.io/@th0566/Javascript-얕은-복사-깊은-복사](https://velog.io/@th0566/Javascript-%EC%96%95%EC%9D%80-%EB%B3%B5%EC%82%AC-%EA%B9%8A%EC%9D%80-%EB%B3%B5%EC%82%AC){:target="_blank"}