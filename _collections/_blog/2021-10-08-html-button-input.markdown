---
layout: post
title:  "[HTML] button 태그와 input type="submit"과의 차이 "
author: Kenna
date:   2021-10-08 11:26:35 +0830
image: https://images.unsplash.com/photo-1592825508076-d59e805443cc?ixid=MnwxMjA3fDB8MHxzZWFyY2h8OTh8fGNvb2tpZXN8ZW58MHx8MHx8&ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60
rating: 60
description: [HTML] button 태그와 input type="submit"과의 차이
categories : HTML
tags: HTML
---

###### `<button>` 과 `<input type="submit">`의 차이

<br>

`<button>` 과 `<input type="submit">`의 차이를 자바스크립트의 필요 유무로 나누면 아래와 같다. 
<br>


**자바스크립트 필요** -> `<button>`,`<input type="button">`
<br>

`<button>` 으로 작성한 버튼은 자바스크립트로 작성한 양식을 전송한다.  
type의 기본값은 submit이지만 반드시 submit에 사용되지 않는 경우도 있기 때문에 type은 가능하면 명시하는 것이 추후 유지보수에 좋다.  

<br>

*클릭 이벤트 시 type*
submit : 데이터 제출 버튼
reset : form 내부의 모든 값을 초기화
button : 클릭 이벤트에서 실행할 것을 자바스크립트로 설정한다.


`<input type="button">`도 자바스크립트와 함께 사용하는 버튼을 의미한다.

두 개의 차이는 태그 안에 다른 태그를 넣을 수 있는가? 이다.
`<button>`태그는 `<button></button>` 으로 표현되는 끝이 닫히는 태그로 다른 요소를 안에 넣어 다양하게 꾸밀 수 있지만  
`<input>`은 끝을 닫는 태그가 아니다.(*참고 'self-closing tag')
<br>

또한 기존에 `<button>`태그는 구형 브라우저에서 지원이 되지 않아 `<input type="button">`으로 많이 사용되었지만   
지금은 `<button>`태그에 type을 쓰는 것으로 더 많이 사용된다.  

<br>
<br>

**자바스크립트 불필요 -> `<input type="submit">`**
<br>

`<input type="submit">`은 자바스크립트를 사용할 필요없이 form의 action으로 선언한 곳으로 바로 양식이 전송된다.  

<br>
<br>

**form 요소의 기본 구성**
<br>

*간단하게 아래와 같은 구성으로 기본적인 표준과 접근성을 챙길 수 있다.*  
*속성를 제외하고 뼈대만*  
*p 태그로 내부의 단락을 나눌 수 있다.*
 
<br>

```html
<form>
    <fieldset>
        <input>
        <label>
        <button>
    </fieldset>
</form>
```

참고한 글  
[w3school]('https://www.w3schools.com/TAGS/att_input_type_button.asp')  
[365kim님의 글]('https://365kim.tistory.com/64')
