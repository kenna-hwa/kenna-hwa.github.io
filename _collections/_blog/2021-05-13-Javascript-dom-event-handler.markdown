---
layout: post
title:  "[Javascript DOM] 이벤트와 DOM"
author: Kenna
date:   2021-05-13 21:30:35 +0830
image: https://images.unsplash.com/photo-1586162481176-7abc53f1f7c2?ixid=MnwxMjA3fDB8MHxzZWFyY2h8ODZ8fHN0dWR5fGVufDB8fDB8fA%3D%3D&ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60
rating: 3
description: 수업 복습
---


###### 사용자 정의 함수

- 사용자가 임의로 생성한 함수

- 선언문 : function

- function 함수명 (매개변수, 매개변수...) {
    실행문
    실행문
    .
    .
  }

- 함수는 호출 시에만 실행된다.
    - 단독으로 실행
    - 변수에 의해 실행
    - 다른 함수에 의해 실행
    - 이벤트에 의해 실행<br><br>

- 함수명 규칙은 변수명 생성 규칙과 같다.

- 함수 내 혹은 파라미터(매개변수) 안에 br 태그가 필요한 경우 이스케이프 문자 (\n) 를 사용한다.



###### 이벤트

- 이벤트는 상황이라는 뜻, ~~하는 행위를 나타낼 때 사용한다.
    - load
    - unload
    - mouseover
    - mouseout
    - focus
    - blur
    - click
    - mousedown
    - mouseup<br><br>

- 이벤트핸들러 EventHandler : 이벤트 사용 시. ~~ 했을 때. 이벤트 명 앞에 on 을 추가한다.
    - onload
    - onunload
    - onmouseover
    - onmouseout
    - onfocus
    - onblur
    - onclick
    - onmousedown
    - onmouseup

최종 문법
=> obj.eventHandle = function(){}


function testFunc() {<br>
        alert("함수를 실행하였습니다.")<br>
}
<br><br>
위의 함수를 실행해본다. 


- 함수 이름으로 실행

    testFunc();

- 변수에 넣어 실행

    let i = testFunc();

- 다른 함수에 의해 실행

    setTimeout("testFunc()", 1000);<br>
    setTimeout은 ms단위의 시간 이후에 첫번째 파라미터에 들어가 있는 함수를 실행하는 내장함수


###### DOM (Document Object Model)

- HTML 요소에 접근하는 표준화된 방식

- 기존 name 속성과 태그별 접근 방식에서 벗어나 오브젝트(요소, tag, element)의 종류에 상관없이 id, class 속성을 사용하여 요소에 접근하는 방식

<br>

###### getElementById("element#id") 객체의 생성

- DOM 코어 / HTML - DOM

- DOM 코어 : 스크립트가 지원되는 모든 기기에서 사용
- HTML - DOM : 웹 브라우저에서만 사용 가능

---------------------------------------------------------------------


*body 안에 html 요소

form name="form1" action="" method=""
    input type="text" name="txt" id="txt"
    button type="button" onclick="printText()


---------------------------------------------------------------------

- function으로 html의 form 요소 선택하는 기존 방식 : 배열 or form의 name 속성값<br>
    document.formName.txt.value

- getElementById 방식으로 요소 선택하는 방식<br>
    document.getElementById("txt").value



스타일을 바꿔야 하는 경우 .style.PROPERTY 로 적용할 수 있는데 이 때 PROPERTY 값은 대쉬로 연결된 경우 카멜텍스트로 변경해서 사용해야 한다.<br>
ex font-size -> fontSize

또한 인라인 스타일, id 선택자 방식, class 선택자 방식, 요소 선택자 방식이 혼재했을 경우

  요소  -------- 1점<br>
 class --------- 10점<br>
  id   -------------------- 100점<br>
인라인 ---------- 1000점<br>
<br>
!important ---------- 10000점

우선 순위가 다르기 떄문에 스타일이 적용되는 방식은 반드시 한가지 스타일로 통일해야 한다.


