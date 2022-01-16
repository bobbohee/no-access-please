---
layout: post
category: etc
---

# 문제

크게 디자인이 필요하지 않은 웹페이지는 부트스트랩을 사용해 디자인을 하곤 한다.
많은 것 중 grid와 spacing(margin과 padding)을 가장 많이 사용하는데, 공식 문서를 보면 margin과 padding 마이너스 값을 입력할 수 있는 방법은 없다.

👉 [bootstrap 공식 문서 - spacing 표기법](https://getbootstrap.com/docs/4.0/utilities/spacing){:target="_blank"}

# 해결

숫자 앞에 `n`을 붙이면, 음수 값으로 인식된다.

```html
<div class="mt-n2" style="width: 200px;">
  Centered element
</div>
```

# 참고

[https://stackoverflow.com/questions/51282923/bootstrap-negative-margin-on-rows](https://stackoverflow.com/questions/51282923/bootstrap-negative-margin-on-rows){:target="_blank"}
