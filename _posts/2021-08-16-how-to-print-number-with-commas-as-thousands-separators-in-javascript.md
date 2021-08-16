---
layout: post
category: etc
---

# 문제

숫자(금액)을 흔히 나타낼 때, 숫자 3자리마다 ,(콤마)를 찍어 나타낸다. `ex) 45,000`

# 해결

## 방법1

```javascript
const num = 23040;
num.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ',');
// 출력 : 23,040
```

## 방법2

```javascript
const num = 7600;
num.toLocaleString();
// 출력 : 7,600
```

# 참고

[https://stackoverflow.com/questions/2901102/how-to-print-a-number-with-commas-as-thousands-separators-in-javascript](https://stackoverflow.com/questions/2901102/how-to-print-a-number-with-commas-as-thousands-separators-in-javascript){:target="_blank"}