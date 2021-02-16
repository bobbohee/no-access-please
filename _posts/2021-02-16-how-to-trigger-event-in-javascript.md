---
layout: post
category: javascript
---

# 문제

관련 검색어 리스트를 보여주는 A 클래스와 검색 결과 리스트를 보여주는 B 클래스로 분리되어있다. 
검색어 입력폼에서 keydown(enter) 이벤트 발생 시, 검색 결과 리스트를 B 클래스에서 생성하는데 관련 검색어 리스트 중 1개를 클릭 시, A 클래스에서 해당 관련 검색어로 검색 결과 리스트를 생성해야 한다.
기존은 A 클래스에서 B 클래스에 검색 결과 리스트 생성 메소드를 호출하도록 했지만, 두 클래스 간의 종속성을 없애고자 했다.


기존 코드 

```javascript
class A {
    constructor() {
        this.b = new B();
    }
    
    clickRelatedKeyword() {
        this.b.createSearchResult();
    }
}
```

# 해결

검색어 입력폼에서 keydown(enter) 이벤트 발생 시, 검색 결과 리스트를 B 클래스에서 생성하기 때문에 강제로 keydown(enter) 이벤트를 발생시켜 해결했다.

```javascript
class A {
    constructor() {
    }

    forceEnterEvent() {
        const keyword = document.querySelector('input[name="keyword"]');

        let event;
        const eventType = 'keydown';
        const enter = 13; // Enter키 keycode

        // IE 9, Chrome, Firefox
        if (document.createEvent) {
            event = document.createEvent('HTMLEvents');
            event.keyCode = enter;
            event.initEvent(eventType, true, true);
            keyword.dispatchEvent(event);
        }
        // IE 8
        else {
            event = document.createEventObject();
            event.keyCode = enter;
            event.eventType = eventType;
            keyword.fireEvent(`on${eventType}`, event);
        }
    }
    
    clickRelatedKeyword() {
        this.forceEnterEvent();
    }
}
```

# 참고 사이트

[https://stackoverflow.com/questions/2490825/how-to-trigger-event-in-javascript](https://stackoverflow.com/questions/2490825/how-to-trigger-event-in-javascript){:target="_blank"}

[https://plainjs.com/javascript/events/trigger-an-event-11](https://plainjs.com/javascript/events/trigger-an-event-11){:target="_blank"}