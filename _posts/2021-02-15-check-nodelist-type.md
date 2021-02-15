---
layout: post
category: javascript
---

# 문제

메소드에 타입 예외 처리를 하고, 일부 메소드 명을 수정하니 작동하던 기능에서 오류가 났다.

# 원인

타입 예외 처리에서 `NodeList`가 배열로 이루어져 있기 때문에 배열로 타입 검사를 한 게 문제였다. 

기존 코드

```javascript
class Common {
    isArray(value) {
        return Array.isArray(value);
    }
    
    /**
     * @param {NodeList} els
     */
    removeClass(els) {
        const _t = this;
        if (!_t.isArray(els)) return;
            
        // ... code
    }
}
```

# 해결

NodeList 타입 검사 메소드를 추가해 바꾸었다.

```javascript
class Common {
    isNodeList(value) {
        return NodeList.prototype.isPrototypeOf(value);
    }
    
    /**
     * @param {NodeList} els
     */
    removeClass(els) {
        const _t = this;
        if (!_t.isNodeList(els)) return;
            
        // ... code
    }
}
```

👉 [Node 타입 검사](https://stackoverflow.com/questions/185034/testing-the-type-of-a-dom-element-in-javascript){:target="_blank"}

# 참고 사이트

[https://stackoverflow.com/questions/7238177/how-to-detect-htmlcollection-nodelist-in-javascript/39965818](https://stackoverflow.com/questions/7238177/how-to-detect-htmlcollection-nodelist-in-javascript/39965818){:target="_blank"}
