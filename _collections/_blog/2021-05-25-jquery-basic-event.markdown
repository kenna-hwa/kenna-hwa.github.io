---
layout: post
title:  "[jQuery] jQuery Event"
author: Kenna
date:   2021-05-25 16:26:35 +0830
image: https://images.unsplash.com/photo-1503437313881-503a91226402?ixid=MnwxMjA3fDB8MHxzZWFyY2h8MTR8fGNvZGV8ZW58MHx8MHx8&ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60
rating: 9
description: W3C | jQuery 문서
---

###### 제이쿼리 jQuery Event
[W3C 공부하러가기]("https://www.w3schools.com/jquery")

###### DOM EVENT 종류

- Mouse
    - click : 한 번 클릭
    - dblclick : 더블클릭
    - mouseenter : 마우스 커서 오버
    - mouseleave : 마우스 커서 오버 후 커서가 나갔을 때

- Keyboard
    - keypress : 키보드 키를 누를 때 *현재는 deprecated
    - keydown : 키보드 키를 누를 때
    - keyup : : 키보드 키를 누르고 뗄 때

- Form
    - submit : 폼 양식 제출(전송)
    - change : 폼 양식 변경
    - focus : 입력하기 위해 양식에 포커스가 적용되었을 때
    - blur : 양식에서 포커스가 제거되었을 때

- Document/Window Events
    - load : 문서 로드
    - resize : 문서의 브라우저 사이즈가 변경되었을 때
    - scroll : 문서에서 스크롤이 일어났을 때
    - unload : 문서 종료

###### jQuery에서 Event 사용

**click()**<br>
selector로 선택한 element를 클릭하면 이벤트 발생

<pre>$("selector").click(function(){ // 클릭하면 발생할 이벤트 함수 코드 입력 });
</pre>

**dblclick()**<br>
selector로 선택한 element를 더블클릭하면 이벤트 발생

<pre>$("selector").dblclick(function(){ // 더블클릭하면 발생할 이벤트 함수 코드 입력 });
</pre>


**mouseenter()**<br>
selector로 선택한 element에 마우스를 오버시키면 이벤트 발생

<pre>$("selector").mouseenter(function(){ // 마우스 오버하면 발생할 이벤트 함수 코드 입력 });
</pre>

**mouseleave()**<br>
selector로 선택한 element에 마우스를 올렸다가 내리면 이벤트 발생

<pre>$("selector").mouseleave(function(){ // 마우스를 올렸다 내리면 발생할 이벤트 함수 코드 입력 });
</pre>

**mousedown()**<br>
selector로 선택한 element에 마우스의 어떤 버튼을 클릭했을 때 바로 이벤트 발생

<pre>$("selector").mousedown(function(){ // 마우스 클릭, 우클릭, 또는 휠 클릭하자마자 발생할 이벤트 함수 코드 입력 });
</pre>

**mouseup()**<br>
selector로 선택한 element에 마우스의 어떤 버튼을 클릭했다가 손을 뗄 때 이벤트 발생

<pre>$("selector").mouseup(function(){ // 마우스 클릭, 우클릭, 또는 휠 클릭하고 뗄 때 발생할 이벤트 함수 코드 입력 });
</pre>

**hover()**<br>
selector로 선택한 element에 마우스를 올렸다가 내리면 이벤트 발생<br>
mouseenter와 mouseleave가 합쳐진 조합으로 두 개의 이벤트 함수 사용<br>

<pre>$("selector").hover(function(){ // 마우스를 올리면 발생할 이벤트 함수 코드 입력 },
function(){ // 마우스를 내리면 발생할 이벤트 함수 코드 입력 });
</pre>

**focus()**<br>
selector로 선택한 input과 같은 입력 element에 포커스가 적용되었을 때 이벤트 발생

<pre>
$("selector").focus(function(){ // 입력 포커스가 적용되었을 때 발생할 이벤트 함수 코드 입력});
</pre>

**blur()**<br>
selector로 선택한 input과 같은 입력 element에 포커스가 빠져나왔을 때 이벤트 발생

<pre>
$("selector").blur(function(){ // 입력 포커스가 빠져나왔을 때 발생할 이벤트 함수 코드 입력});
</pre>

**on()**<br>
selector로 선택한 element에 하나 이상의 이벤트를 연결

<pre>
$("selector").on("click", function(){ // click 이벤트 이후 발생할 이벤트 함수 입력});
</pre>

<pre>
$("selector").on({
                event1: function(){
                  $(this).css("");
                },
                event2: function(){
                  $(this).addClass("");
                },
                event3: function(){
                  $(this).removeClass("");
                }
              });
</pre>
처럼 사용할 수도 있음



