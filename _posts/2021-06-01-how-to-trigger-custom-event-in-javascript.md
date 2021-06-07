---
layout: post
category: javascript 
---

# 해결

A 클래스에서 B 클래스의 함수를 사용하는데 두 클래스 간의 종속성을 가져가지 않고, 꼼수(?)를 부리는 방법으로 `CustomEvent`를 사용했다. 

<br>

아래 예제는 A 클래스에서 B 클래스의 길찾기 생성을 위한 `_drawRoute()`함수를 사용하기 위한 예제이다.

<br>

🌟 CustomEvent를 통해 넘겨주고 싶은 값이 있다면 `detail`을 사용해 넘길 수 있다.  

```javascript
// A.js - 이벤트 등록
class A {
    
    _triggerEvent() {
        const elem = document.querySelector('#start_route');

        const event = new CustomEvent('route', {
            detail: {
                coordinate: [37.553115, 127.006273],  
            }
        });
        
        elem.dispatchEvent(event);
    }

}
```


```javascript
// B.js - 이벤트 처리
class B {
    
    _drawRoute(coordinate) {
        // 길찾기 처리
    }

    _onRoute(e) {
        this._drawRoute(e.detail.coordinate);
    }

    event() {
        const elem = document.querySelector('#start_route');

        elem.addEventListener('route', (e) => this._onRoute(e));
    }

}
```

# 참고

[https://developer.mozilla.org/en-US/docs/Web/Events/Creating_and_triggering_events](https://developer.mozilla.org/en-US/docs/Web/Events/Creating_and_triggering_events){:target="_blank"}
