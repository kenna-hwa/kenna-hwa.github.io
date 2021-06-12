---
layout: post
title:  "[Javascript DOM] DOM과 querySelector"
author:  Kenna
date:   2021-05-20 21:40:35 +0830
image: https://external-content.duckduckgo.com/iu/?u=https%3A%2F%2Ftse3.mm.bing.net%2Fth%3Fid%3DOIP._WzzKR8jCL6UXF0KC-haGwHaE7%26pid%3DApi&f=1
rating: 8
description: 네이버 부스트코스 강의 정리
categories : [DOM]
tags: [DOM]
---


###### DOM과 querySelector
[부스트코스 강의 보러가기]("https://www.boostcourse.org/web316/lecture/16699/?isDesc=false")

###### DOM

브라우저에서 HTML를 DOM Document Object Model이라는 트리 모양의 객체 형태의 모델로 저장한다.

HTML로 작성한 문서는 변경된다. 
잦은 변경을 쉽게 하려면 어떤 구조체 형태가 되는 것이 좋기 때문에 DOM이라는 모델을 도입한 것.

브라우저에서 DOM을 쉽게 만지고 찾고 조작하도록 여러가지 메서드가 있는 DOM API를 제공한다.

그 메서드들이 바로 **↓↓↓↓↓↓**


------------------------------


**getElementById()**<br>
()안에 id 값을 통해찾을 수 있다.
document.getElementById("아이디값")

만약 스타일을 바꾸고 싶다면
<pre>
<code>
document.getElementById("id").style.display="none"
</code>
</pre>
과 같은 모양으로 바꿔주면 된다.
.은 ~에 라는 뜻으로 이해해주면 된다.



**Element.querySelector()**<br>
DOM을 찾는데 유용한 메서드이다. 
CSS스타일을 결정하거나 Selector 문법을 활용해 DOM에 접근할 수 있다. 
() 안에 엘리먼트 요소를 넣거나 #아이디값 .클래스값으로 요소를 찾아낼 수도 있다.
#, ., > 등은 CSS selector라고 부른다.

적용은
<pre>
<code>
Element.querySelector("element").style.background="red"
</code>
</pre>
같은 모양으로 바꿔줄 수 있다.



**Element.querySelectorAll()**도 있다.
내가 원하는 요소를 넣으면 문서 안에 모든 요소가 전부 나오기 때문에 for문으로 이용할 때 사용한다.

**CSS Selector**<br>
Selector 문법은 querySelector와 querySelectorAll 메서드에서 사용할 수 있다.

- 범용 선택자 **'*'**
    모든 요소를 선택한다.
- 유형 선택자 **elementName**
    주어진 노드 이름을 가진 모든 요소를 선택한다.
- Class 선택자 **.**
    주어진 class 속성을 가진 모든 요소를 선택한다.
- ID 선택자 **#**
    주어진 Id 속성을 가진 요소를 선택한다. id는 유일해야 한다.
- 속성 선택자 **[attr]**
    주어진 속성을 가진 모든 요소를 선택한다. 
- 선택자 목록 **,**
    쉼표로 연결해 요소를 선택한다.
- 하위 결합자 **A B**
    첫번째 요소의 자손을 연결한다.
- 자식 결합자 **A > B**
    요소의 자식을 연결한다. 
- 일반 형제 결합자 **A ~ B**
    형제 관계에 있는 요소를 연결한다.
- 컬럼 결합자 **A || B**
    컬럼 요소를 연결한다.
- 가상 클래스 **:a**
    HTML요소를 직접적으로 선택하지 않고 요소의 상태에 따라 선택적으로 꾸며준다.
- 가상 요소 **::a**
    단일 선택자 뒤에 추가하여 선택한 요소의 일부분에 스타일을 줄 수 있다. 하나의 선택자에는 하나의 가상 요소만 사용 가능하다.