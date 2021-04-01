---
layout: post
category: jekyll 
---

# 문제

일반적으로 jekyll에서 변수를 선언할 때, `assign` 키워드를 사용한다.

```
{% raw %}
{% assign name = "bobbohee" %}
{{ name }}            # bobbohee
{% endraw %}
```

<br>

각각 name과 age 변수를 생성하고, about_me 변수에 name과 age, 2개 변수를 사용해 소개 문구를 작성해보자.

출력만 하면 된다면 상관없겠지만, `assign`은 2개의 변수 값을 담을 수 없다.

```text
{% raw %}
{% assign name = "bobbohee" %}
{% assign age = "21" %}

# 출력만 할 경우
I am {{ name }}, {{ age }} 

# 변수에 담을 경우, (사용할 수 없는 방식)
{% assign about_me = I am {{ name }}, {{ age }} %}

{{ about_me }}
{% endraw %}
```

# 해결

`capture`를 사용하면, 여러 변수와 문자열을 포함한 복합 문자열을 변수에 저장할 수 있다. 

```text
{% raw %}
{% assign name = "bobbohee" %}
{% assign age = "21" %}

{% capture about_me %}
    I am {{ name }}, {{ age }}
(% endcapture %)

{{ about_me }}                          # I am bobbohee, 21
{% endraw %}
```


# 참고 

[https://shopify.github.io/liquid/tags/variable](https://shopify.github.io/liquid/tags/variable){:target="_blank"}
