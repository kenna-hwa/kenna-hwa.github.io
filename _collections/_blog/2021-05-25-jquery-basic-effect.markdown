---
layout: post
title:  "[jQuery] jQuery Effect"
author: Kenna
date:   2021-05-25 17:26:35 +0830
image: https://images.unsplash.com/photo-1503437313881-503a91226402?ixid=MnwxMjA3fDB8MHxzZWFyY2h8MTR8fGNvZGV8ZW58MHx8MHx8&ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60
rating: 10
description: W3C | jQuery 문서
---

###### 제이쿼리 jQuery Effect
[W3C 공부하러가기]("https://www.w3schools.com/jquery")

###### jQuery Effect

- hide() : HTML 요소를 숨긴다.

<pre>
  $("selector").click(function(){
    $("selector").hide(speed,이벤트 콜백 함수)
  })
</pre>

- show() : HTML 요소를 나타나게 한다.

<pre>
  $("selector").click(function(){
    $("selector").show(speed,이벤트 콜백 함수)
  })
</pre>

- toggle() : 위의 hide와 show effect를 반복한다.

<pre>
$("selector").click(function(){
  $("selector").toggle(speed,이벤트 콜백 함수)
})
</pre>

**speed에는 숫자와 문자로 시간을 표현할 수 있다. (1000, 1ms, 1s, "slow", "fast" ...)**
