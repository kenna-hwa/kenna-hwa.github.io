---
layout: post
title:  "[Javascript DOM] Browser Event, Event object, Event handler"
author:  Kenna
date:   2021-05-20 22:40:35 +0830
image: https://external-content.duckduckgo.com/iu/?u=https%3A%2F%2Ftse3.mm.bing.net%2Fth%3Fid%3DOIP._WzzKR8jCL6UXF0KC-haGwHaE7%26pid%3DApi&f=1
rating: 9
description: 네이버 부스트코스 강의 정리
---


###### Browser Event, Event object, Event handler
[부스트코스 강의 보러가기]("https://www.boostcourse.org/web316/lecture/16700/?isDesc=false")


**Event**<br>

브라우저 화면에서 발생하는 이벤트
- 화면의 크기를 마우스로 조절하기
- 스크롤 내리기
- 버튼 클릭하기
- 화면 새로고침하기
- 동영상 재생하기
- 링크에 밑줄 생기기 등

브라우저를 사용자가 이용하다 이벤트가 발생하면 브라우저는 이벤트를 개발자에게 알려줄 수 있다.

HTML의 요소별로 키보드나 마우스가 관련된 이벤트가 발생했을 때 특정 행위를 하고 싶다고 자바스크립트를 통해 등록해줄 수 있다.


**이벤트 등록**<br><br>

**addEventListner**

<pre>
<code>
var el = document.querySelector(".outside");
el.addEventListener("click".function(){
    //do something
}, false);
</code>
</pre>

addEventListener 함수의 첫번째 인자는 이벤트 타입Event type이고 두번째 인자는 함수를 갖는다. 세번째 인자는 옵션(useCapture)으로 호환성을 위해 false를 지정한다. 
*이벤트 리스너가 등록된 해당 DOM엘리먼트에 실제 이벤트가 발생했을 때 어떤 순서로 부모 DOM에 전파가 되는지 결정한다.
과거 여러 브라우저가 통일된 규칙을 가지지 않았을 때 이벤트의 전파 순서가 달라 이를 구분해서 사용하기 위한 인자다. -> 이벤트 버블링과 관련

**선행되어야 할 것은 먼저 이벤트를 등록해 줄 요소를 지정해야한다는 것이다.**
요소를 선택한 후 이 요소에 이벤트 함수를 작성해줄 수 있다.

**요소.이벤트 함수**
<br>

이 함수는 나중에 이벤트가 발생할때 실행될 함수로 **콜백함수** 이며 
**이벤트 핸들러(Event Handler) 혹은 이벤트 리스너(Event Listener)** 라고 부른다.

**이벤트 객체**<br><br>

브라우저는 이벤트 리스너를 호출할 때 사용자로부터 어떤 이벤트가 발생했는지 정보를 담은 이벤트 객체를 생성해 이벤트 함수에 전달한다. 
이 이벤트 객체를 변수에 담을 수 있고 이벤트 객체를 이용해서 추가적인 작업을 할 수 있다.

가장 많이 쓰이는 이벤트 객체는 **event.target**이다.

e.target으로 변수에 담아 두고 변수를 이용해서 다양한 정보를 확인할 수 있다.


-------------------

- Event type 알아보기

    1. 윈도우 이벤트
        - load : 웹페이지의 로드가 완료되었을 때
        - unload : 웹 페이지가 언로드 될 때
        - error : 브라우저가 자바스크립트 오류를 만났을 때
        - resize : 브라우저의 창 크기를 조정했을 때
        - scroll : 사용자가 페이지를 위 아래로 스크롤 할 때
    2. 마우스 이벤트
        - click : 마우스 버튼을 클릭했다 뗄 때
        - dbclick : 마우스 버튼을 두 번 연속 더블 클릭할 때
        - mousedown : 마우스 버튼을 누르고 있을 깨
        - mouseup : 눌렀던 마우스 버튼을 뗄 때
        - mouseout : 요소 위로 마우스를 움직였을 때
        - mouseover : 요소 바깥으로 마우스를 움직였을 때
    3. 키보드 이벤트
        - keydown : 키를 누르는 순간
        - keyup : 키를 눌렀다 떼는 순간
        - keypress : 키를 눌러 문자가 입력되었을 때
    4. 포커스 이벤트
        - focus : 요소에 포커스가 갔을 때
        - blur : 요소가 포커스에서 벗어났을 떄
    5. 폼 이벤트
        - submit : 전송 버튼을 눌렀을 때 또는 텍스트 필드에서 엔터키를 눌렀을 때
        - reset : 폼을 초기화 하기 위함
        - change : 폼 필드에서 변경이 일어났을 때
        - select : option 태그에서 option이 선택되었을 때