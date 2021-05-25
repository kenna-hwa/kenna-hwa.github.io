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

**hide, show, toggle**<br>

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

speed에는 숫자와 문자로 시간을 표현할 수 있다. (1000, 1ms, 1s, "slow", "fast" ...)

**Fading**<br>

- fadeIn() : 선택한 HTML 요소가 서서히 나타난다.

<pre>
$("selector").fadeIn(speed)
</pre>

- fadeOut() : 선택한 HTML 요소가 서서히 사라진다.

<pre>
$("selector").fadeOut(speed)
</pre>

- fadeToggle() : 선택한 HTML 요소가 서서히 나타났다 사라지는 것을 반복한다.

<pre>
$("selector").fadeToggle(speed)
</pre>

- fadeTo() : 선택한 HTML 요소가 불투명하게 사라지게 할 수 있다. 불투명도는 **0-1**사이로 조절한다.

<pre>
$("selector").fadeTo(speed, opacity)
</pre>

**silding**<br>

- slideDown() : 선택한 HTML 요소가 아래로 슬라이딩한다.

<pre>
$("selector").slideDown(speed)
</pre>

- slideUp() : 선택한 HTML 요소가 위로 슬라이딩한다.

<pre>
$("selector").slideUp(speed)
</pre>

- slideToggle() : 선택한 HTML 요소의 슬라이드가 반복된다.

<pre>
$("selector").slideToggle(speed)
</pre>

**animate**<br>

- animate() : 선택한 HTML 요소가 움직인다.

<pre>
$("selector").animate({parameter}, speed, 작동할 함수)
</pre>

parameter에는 css 속성을 넣을 수 있다.
css속성이 대쉬(-)로 이어져 있으면 카멜 케이스Camel Case로 작성하면 적용된다.
색상 css는 jQuery 라이브러리를 다운받아야 한다.
속성값에는 ''따옴표를 붙여야 한다. (전체가 ""큰 따옴표로 덮여 있기 때문에)

**animate로 요소를 움직이고 싶으면 해당 요소에 position이 설정되어 있어야 한다.**

**stop**<br>

- stop() : 움직이던 HTML 요소를 멈추게 할 수 있다.

<pre>
$("selector").stop()
</pre>

stop() 메소드는 현재 수행되는 animation을 멈추는데 주로 사용되어 중복해서 사용하기도 한다.

<pre>
$("selector").stop().slideDown()
</pre>


