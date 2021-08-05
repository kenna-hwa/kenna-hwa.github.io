---
layout: post
title:  "[Javascript] 모달Modal창 만들기"
author: Kenna
date:   2021-08-04 21:26:35 +0830
image: https://images.unsplash.com/photo-1593720219276-0b1eacd0aef4?ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&ixlib=rb-1.2.1&auto=format&fit=crop&w=1343&q=80
rating: 43
description: Javascript로 모달Modal창 만들기
categories : Javascript
tags: Javascript
---

###### 자바스크립트로 모달창 구현하기

웹에 포트폴리오를 올려놓고나니 클론 코딩한 페이지에는  
안내를 하는 문구가 있으면 좋겠다는 생각을 했다.  
링크를 들어가서 window가 로딩되자 마자 모달창을 클릭해야 내가 만든 페이지를 볼 수 있는 모달창을 만들어보자.

<br>
모달창 구현은 생각보다 간단한 구조인데 나중에 ajax를 써서 뭔가를 입력받는다거나 하면 그땐 좀 머리아플거 같긴 하다 ....
<br>

우선 HTML 아무데나(헤더 위에도 괜찮을듯 문서 구조상 먼저 나오니) HTML 코드를 만든다.
div로 브라우저 전체를 다 감싸서 배경을 만들고,  
다시 내부에 작은 창을 띄워 닫기 버튼을 클릭하면 div가 `display: none;`이 되는 구조다.
  <br>
CSS만 적당히 잘 입히면 스크립트 코드는 어렵지 않음!  

<br>
그리고 모달창 닫기를 클릭해야 스크롤이 내려갈 수 있는 코드도 작성해야   
브라우저 window에 보이는 부분 외의 기능이 동작하는 모습을 보여주지 않을 수 있다.

<br>

**HTML**<Br>

<br>

```html
<div class="modal_wrap">
	<div class="modal">
		<p>
			지금 보시는 페이지는 실제 기업의 페이지가 아닌  <br>
            개인 포트폴리오용으로 제작되었습니다. <br>
			© 2021 Juhwa Hwnag. All Rights Reserved. <br>
		</p>
        <button type="button" class="modal_close_btn">닫기</button>
	</div>
</div>
```


<br>

**CSS**<Br>

<br>

```css
.modal_wrap { 
position: absolute; 
width: 100%; 
height: 100%; 
top: 0; 
left: 0; 
background-color: rgba(50, 50, 50, 0.4); 
} 

.modal { 
position: absolute; 
width: 400px; 
height: 600px; 
top: 50%; 
left: 50%; 
padding: 40px;
text-align: center; 
background-color: white;
border-radius: 10px; 
box-shadow: 0 2px 3px 0 rgba(150, 150, 150, 0.2); 
transform: translateX(-50%) translateY(-50%); 
}

.modal_close_btn{
    margin-top: 35px;
    font-size: 18px;
    color: palevioletred;
    font-weight: 600;
}
.modal_wrap.active { 
display: block; 
} 
    

```
<br>

**Javascript**<Br>

<br>

```jsx
const body = document.querySelector('body'); 
const modal = document.querySelector('.modal_wrap'); 
const closeBtn = document.querySelector('.modal_close_btn');

window.addEventListener('load', () => {
    modal.classList.add('active');

    if (modal.classList.contains('active')) {
        body.style.overflow = 'hidden';
    }
  });

  closeBtn.addEventListener('click', () => {
      modal.classList.remove('active');

      if (!modal.classList.contains('active')) {
        body.style.overflow = 'auto';
    }
  });
```

body를 잡은 이유는 모달 창이 떠있는 동안에는 스크롤이 내려가지 않게 하려고 body에 `overflow:hidden;`을 주었고  
window가 로드 되면 modal_wrap이라는 클래스에 active라는 클래스가 추가된다.  
modal_wrap에 active가 붙으면 modal_wrap div가 `display: block;` 된다.
따라서 window가 로드되면서 모달창이 나타난다.

<br>

이 때 body에 `overflow:hidden;`이 먹히도록 if문으로 modal_wrap의 클래스 중에 active가 있으면 body에 `overflow:hidden;`를 만드는 조건문을 넣는다.

<br>

그리고 닫기 버튼 클래스인 closeBtn에 click 이벤트를 주고  
modal_wrap에서 active 클래스를 remove 한다. 그러면 modal_wrap이 `display: none;` 으로 원상복구된다.  

그리고 아까와 마찬가지로 if문으로 modal_wrap 클래스 리스트 중 active가 없으면 body에 `overflow: auto;` 기본값으로 바뀌도록 한다.

<br>

아이콘과 버튼을 이용한 모달창은 여기서 확인 가능  
<br>


[모달창 확인하기](http://kenna.dothome.co.kr/mobilefirst/)