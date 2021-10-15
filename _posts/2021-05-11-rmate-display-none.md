---
layout: post
category: etc
---

# 문제

시흥시 교통약자이동지원센터의 데이터를 분석해 rMate 차트로 나타내고자 했다. 

퍼블리싱이 완료될 동안 다른 페이지에서 차트를 나타내는 작업을 완료했고, 퍼블리싱이 완료된 후 페이지에 넣었는데 다른 페이지에서 잘 나오던 차트가 나오지 않았다. 
문제를 알아보기 위해 크롬에 개발자 모드를 여는 순간, 신기하게도 차트가 나타났다. 조금 더 테스트 한 결과 브라우저의 가로 길이가 변경되니 차트가 나타남을 알 수 있었다.

<div>
    <img src="/no-access-please/assets/image/2021-05-11-rmate-display-none/1.png" alt="차트 안나타남"/>
    <figcaption>차트 안나타남</figcaption>
</div>

<div>
    <img src="/no-access-please/assets/image/2021-05-11-rmate-display-none/2.png" alt="차트 나타남"/>
    <figcaption>차트 나타남</figcaption>
</div>

# 원인

차트를 생성할 때, 차트의 가로와 세로 길이를 지정하는 속성이 있는데 길이를 100%로 설정했었다. 
100%로 설정한 것이 문제인가 싶어 px로 바꿨더니, 차트 3개 중 1개만 정상적으로 나타나고 2개는 나타나지 않았다.

100%로 설정한 것이 문제가 아니면 `display: none;` 스타일로 인해 발생한 문제라고 생각했다. 
여러 차트 목록에서 클릭했을 때, 해당 차트가 나타나는 방식이었기 때문에 그 전까지는 `display: none;`로 화면에서 안 보이게 해두었다.
이와 관련해 검색했더니 rMate 공식 사이트의 공지사항에서 원인을 찾을 수 있었다. (아래 참고) 

> 화면에 차트를 출력하지 않고 차트의 이미지 데이터를 가져오려 할 경우 : <br>
극히 드문 경우이지만,  아주 드물게 사용하는 이용자가 있어, 안내드립니다.
display:none 해놓은 후 이미지 데이터를 가져오고자 할 경우
left:-1000px와 같이 변경하여 화면에 출력 후 이미지 데이터를 가져오는 방식으로 변경하여 주시기 바랍니다.
display:none 상태에서는 차트의 크기 값들을 올바르게 가져오지 못하여 정상적인 이미지 데이터를 가져오기 힘들기에 
해당 기능을 사용하실 경우에는 기존에 사용하시던 방식을 변경하여 주시기 바랍니다.

`display: none;` 스타일을 제거하니 차트가 정상적으로 나타났다. 

# 참고

[http://www.riamore.net/bbsNew/boards/notice/15558?boardKey=3&boardName=notice&viewType=generic&rows=15&sort=sequence&order=desc&pageNumber=1&messageCategoryKey=&status=&period=&starPointdt=&enddt=&queryField=&query=&messageKey=16316](http://www.riamore.net/bbsNew/boards/notice/15558?boardKey=3&boardName=notice&viewType=generic&rows=15&sort=sequence&order=desc&pageNumber=1&messageCategoryKey=&status=&period=&starPointdt=&enddt=&queryField=&query=&messageKey=16316){:target="_blank"}