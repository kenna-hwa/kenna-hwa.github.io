---
layout: post
title: _collection/_blog/2021-05-14-javascript-queryselector
author: John F. Kennedy
date: '1963-06-26 20:20:35 +0200'
image: 'https://i.ytimg.com/vi/JAAOEC2fV_8/maxresdefault.jpg'
rating: 3
description: 'All free men, wherever they may live, are citizens of Berlin - says JFK.'
published: true
---
---
layout: post
title:  "Javascript QuerySeletor"
author: Kenna
date:   2021-05-14 14:50:35 +0830
image: http://hdblackwallpaper.com/wallpaper/2015/07/black-and-white-landscape-photography-1-background-wallpaper.jpg
rating: 4
description: 수업 복습
---

##### getElementBy

어떤 태그이건 상관 없으나 id 값이 있어야 하고 id 값은 메모리 하나를 차지하기 때문에 때로는 효율이 나쁠수도 있다.

- document.form1.txt_id.value = "이전 방식으로 폼요소 선택하기";

- document.getElementById("idName").value = "아이디 이름으로 선택하기";

- document.getElementsByClassName("ClassName").value = "클래스 이름으로 선택하기";

- document.getElementsByName("Name").value = "태그 이름으로 선택하기";

- document.getElementsByTagName("Tag").value = "태그로 선택하기";

- document.getElementsByTagNameNS("웹사이트의 주소, 태그이름").value = "웹 사이트의 주소, 태그 이름";


##### querySelector

getElementBy 처럼 태그의 종류 상관없으며 값의 입력 방식이 CSS와 같다.
querySelectorAll은 호환이 안되는 경우가 있기 때문에 안정성이 떨어진다.

- document.querySelector(" selector ");

- document.querySelector( "tag" ).value = "쿼리셀렉터 - 태그 이름";

- document.querySelector( "idName" ).value = "쿼리셀렉터 - 아이디 이름";

- document.querySelector( "ClassName" ).value = "쿼리셀렉터 - 클래스 이름";


##### 변수에 담아두기 -> 객체(object)

- 객체(object) 생성 
  var obj = document.getElementById(" idName ");
  
  이제부터 document.getElementById(" idName "); 이 필요한 부분에는 변수 obj를 사용하면된다.
  
  따라서
  
  document.getElementById(" idName ").value 와 obj.value는 같다.
  
  변수에 넣어서 객체로 만들어 두면 문장도 간단해지고 사용하기가 편하다.


##### HTML-DOM

HTML에 **있는** 속성값들로만 사용이 가능하다

- 속성값 가져오기
**객체.속성** 이름으로 속성값을 가져올 수 있다.
obj.attribute_name;
(ex obj.src , 변수이름.type)

- 속성값 변경 & 속성 추가
객체로 지정한 태그 문장에 해당하는 속성이 있으면 값을 바꿔주고 없으면 만들어서 값을 넣어준다.
다만, HTML에서 사용하는 속성만 만질 수 있으며 없는 속성값에는 적용되지 않는다.


##### DOM-CORE

HTML에 **없는** 속성값도 사용 가능하다.

- 속성값 가져오기
**객체.getAttribute("속성이름")** 으로 속성값을 가져올 수 있다.
(ex obj.getAttribute("src")
