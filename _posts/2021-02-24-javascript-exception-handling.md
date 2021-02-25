---
layout: post
category: javascript
---

# 문제

자바스크립트는 에러가 나면 스크립트 자체가 중단되어 버린다.
이런 상황을 막기 위해 예외 처리를 하고자 했다.

# 해결

## 가장 기본! try..catch

가장 기본은 `try..catch`를 사용하는 것이다.

`try`에서 오류가 발생하면서 `catch`로 넘어오게 된다.

```javascript
function sayHelloWorld() {
    try {
        console.log('hello world!');
    } catch (e) {
        console.error(e);
    }
}
```

## 강제 에러

`throw`를 사용해 강제로 오류를 발생시킨다.

```javascript
function say(message) {
    try {
        if (!message) {
            throw new Error(); 
        }
    } catch (e) {
        console.error(e);
    }
}
```

## 커스텀 에러

기존 자바스크립트 에러를 상속받아 나만의 커스텀 에러를 만들 수 있다.

에러를 커스텀해 사용하면 더욱 다양한 처리를 할 수 있다.

**ES6 문법 기준**

```javascript
class CustomError extends Error {
    
    constructor(message) {
        super(message);
        this.name = 'CustomError';
    }
    
    toString() {
        return `${this.name}: ${this.message}`;
    }
    
}
```

# 참고한 사이트

[https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Error](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Error){:target="_blank"}

[https://pks2974.medium.com/javascript%EC%99%80-%EC%97%90%EB%9F%AC-error-d5b1c1124d16](https://pks2974.medium.com/javascript%EC%99%80-%EC%97%90%EB%9F%AC-error-d5b1c1124d16){:target="_blank"}

[https://imkh.dev/js-error](https://imkh.dev/js-error){:target="_blank"}
