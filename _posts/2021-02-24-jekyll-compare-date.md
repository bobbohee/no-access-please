---
layout: post
category: jekyll 
---

# 문제

운영 중인 [개발 블로그](https://park-bohee.github.io/post)에 일주일(7일) 이내에 작성된 포스트에 New 태그를 추가하고 싶었다.

가장 최근 포스트에 New 태그를 추가할까 생각했지만, 포스트를 오랜 시간 작성하지 않으면 몇 달이 지나도 New 태그가 남아있어 이 방식은 옳지 않다고 생각했다.

# 해결

> 예제 코드가 적용되어, 이미지로 대체한다.

## date 형식 변환

포스트를 작성한 날짜와 현재 시간을 출력하면 다음과 같은 date 형식으로 출력된다. 

(블로그 설정마다 출력 형식은 다를 수 있다.)

![date 출력](/no-access-please/assets/image/2021-02-24-jekyll-compare-date/1.svg)

<br>

위 date 형식을 `%s`(`1970-01-01 00:00:00 UTC`을 기준으로 지난 시간(초))으로 변환한다.

![date 형식 변환](/no-access-please/assets/image/2021-02-24-jekyll-compare-date/2.svg)

👉 [Jekyll Date 형식](https://learn.cloudcannon.com/jekyll/date-formatting/){:target="_blank"}

## date 비교

현재 시간(초)에서 포스트를 작성한 시간(초)을 빼고, 시간(초)를 날짜(day)로 변환한다. 

![date 비교](/no-access-please/assets/image/2021-02-24-jekyll-compare-date/3.svg)

## New 태그 등록

일주일(7일) 이내에 작성된 포스트라면 New 태그를 추가하는 조건문을 작성한다.

![date 비교](/no-access-please/assets/image/2021-02-24-jekyll-compare-date/4.svg)

# 참고한 사이트

[https://learn.cloudcannon.com/jekyll/date-formatting](https://learn.cloudcannon.com/jekyll/date-formatting/){:target="_blank"}

[https://stackoverflow.com/questions/31340018/get-the-difference-in-days-between-two-dates-in-jekyll](https://stackoverflow.com/questions/31340018/get-the-difference-in-days-between-two-dates-in-jekyll){:target="_blank"}
