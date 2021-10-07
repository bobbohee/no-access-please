---
layout: post
category: etc
---

# 문제

금형에서 catity(캐비티)와 shot(샷)은 무엇일까 ?

성형 공정 이동표에 필요한 shot(샷) 값을 구하기 위해, `생산량 / 캐비티하고 소수점은 올림`으로 하라고 되어있었다.

그냥 적힌대로 개발할 수도 있지만, 왜 그렇게 해야하는지 아는 것도 개발에 중요하다고 생각하기 때문에 알아보았다.

# 해결

사진으로 보면 이해하기가 쉽다.

![catity(캐비티)와 shot(샷)](/no-access-please/assets/image/2021-10-07-what-is-cavity-and-shot-in-mold/1.jpeg)

1칸을 catity(캐비티)라고 하고, 전체 한 판 찍는 것을 shot(샷)이라고 한다.

`샷 * 캐비티`를 하면 전체 생산량을 구할 수 있듯이, `생산량 / 캐비티`를 하면 샷을 구할 수 있다.


# 참고

[https://m.blog.naver.com/PostView.naver?isHttpsRedirect=true&blogId=ideastories&logNo=220700908088](https://m.blog.naver.com/PostView.naver?isHttpsRedirect=true&blogId=ideastories&logNo=220700908088){:target="_blank"}