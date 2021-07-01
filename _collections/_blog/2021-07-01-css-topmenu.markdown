---
layout: post
title:  "[CSS] TOP 버튼 만들기"
author: Kenna
date:   2021-07-01 22:26:35 +0830
image: https://images.unsplash.com/photo-1511140973288-19bf21d7e771?ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&ixlib=rb-1.2.1&auto=format&fit=crop&w=1267&q=80
rating: 33
description: 포트폴리오용 랜딩페이지 TOP 버튼 만들기
categories : CSS
tags: CSS
---

###### CSS TOP 메뉴 만들기

TOP 버튼을 처음 만들어본다.   
블로그 참고는 이곳에서 [지구별 안내서]("https://aboooks.tistory.com/99")   
<br>

1) a 태그의 만들고 href에 올라갈 곳 지정하기  
   
<pre>

< header class="header" id="header"> < /header>

< a href="#header" class="top">위로 가기< /a>

</pre>

여기서 #는 id값이기 떄문에 필요한 부분에 id 값을 반드시 준다.   

<br>

2) TOP 버튼 위치 정하기   
   
원래 위치가 오른쪽 하단이었기 때문에   
CSS로 position을 fixed를 준 후 양 쪽에 공간을 만든다.   
내가 만드는 랜딩 페이지는 오른쪽 아래쪽에 모두 15px이다.   

<pre>
.top{
    position: fixed;
    width: 35px;
    height: 35px;
    bottom: 15px;
    right: 15px;
    background: url(../images/top.jpg) no-repeat;
    text-indent: -9999px;
}
</pre>
<br>
