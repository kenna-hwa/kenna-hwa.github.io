---
layout: post
title:  "[Javascript] composedPath 사용하여 클릭이벤트 구현"
author: Kenna
date:   2021-08-21 14:26:35 +0830
image: https://images.unsplash.com/photo-1579468118864-1b9ea3c0db4a?ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&ixlib=rb-1.2.1&auto=format&fit=crop&w=1350&q=80
description: 제주코딩베이스캠프 파이널코딩테스트 문제 3번
categories : Javascript
tags: Javascript
---
<br>

###### Event.composedPath()

<br>

[제코베 파이널코딩테스트 강의](https://www.inflearn.com/course/%ED%94%84%EB%A1%A0%ED%8A%B8%EC%97%94%EB%93%9C-%ED%8C%8C%EC%9D%B4%EB%84%90-%EC%BD%94%EB%94%A9%ED%85%8C%EC%8A%A4%ED%8A%B8/dashboard)

<br><Br>

```html
<div class="content-favorite">
    <button class="button-recommend">
        <i class="icon-thumbs-up"></i>
    </button>
    <button class="button-heart">
        <i class="icon-heart"></i>
    </button>
</div>
```

composedPath()는 **이벤트 버블링bubbling** 개념을 이용해  
<strong style="color:red">이벤트의 경로를 배열값으로 반환하는 배열 메소드다.</strong> 
<br>

**이벤트 버블링bubbling**은  
한 요소에 이벤트가 발생하면, 그 요소에 할당된 이벤트 핸들러가 동작하고, 이어서 부모 요소의 핸들러가 동작한다.  
가장 최상단의 조상 요소를 만날 때까지 이 과정이 반복되면서 요소 각각에 할당된 핸들러가 동작한다.  

  

반대의 경우는 *이벤트 캡쳐링capturing*인데 이 경우는 거의 쓰이지 않는다.  
이것은 **이벤트 위임delegation**의 토대가 되는 이벤트 핸들링 개념이다.   

  
상단의 HTML 코드에 이벤트 위임을 적용해  
버튼을 클릭하면 배경색과 이미지가 변경되는 스크립트 작업을 해보자.   

<br>

**script class 객체 만들기**

<br>


우선 모듈로 만들어 둔 `components/index.js` 파일에 class로 Favorite이라는 컴포넌트를 만들고,  
클래스 객체에서 가장 먼저 실행 될 constructor(){} 함수를 만든다.
<br>

```js
//components/index.js

class Favorite{
    construnctor(){
        this.favoriteElement = document.querySelector(".content-favorite");
    }
}
```
<br>

여기에서 **this**는 클래스가 생성할 인스턴스를 가리키고  
인스턴스 내부에 favoriteElement라는 프로퍼티 키와  
그 값으로 document.querySelector(".content-favorite");을 선언한다.

클릭되는 값은 각각 `button-recommend`와 `button-heart` 두 개의 클래스이지만  
`content-favorite`에 적용한다.  
이벤트 위임을 적용하기 위해서다.  


<br>
<br>

**script class 객체에 메소드 만들기**

Favorite 클래스에 constructor() 메소드가 실행된 후 만들어진 프로퍼티에   
addEventListener를 bind 하는 **bindEvents()**라는 함수를 만든다.  
<br>

```js
//components/index.js

class Favorite{
    construnctor(){
        this.favoriteElement = document.querySelector(".content-favorite");
    }


    bindEvents(){
        this.favortieElement.addEventListener('click', (event)=>{

        });
    }
}
```
<br>
<br>

**composedPath() 메소드 사용하기**
<br>


이 bindEvents() 함수에 cPath 상수를 선언하고  
이벤트 핸들러의 event 인자에 **composedPath() 메소드**를 선언해준다.  
event에 composedPath()를 적용하면 **이벤트가 전파되는 경로를 배열값으로 반환**하게 된다.  
composedPath()를 console.log로 찍어보면 다음과 같이 경로를 알 수 있다.  
<br>

```
(11) [i.icon-thumbs-up, button.button-recommend, div.content-favorite, div.content, section.movie, div.movie-container, div#app, body, html, document, Window]
0: i.icon-thumbs-up
1: button.button-recommend.on
2: div.content-favorite
3: div.content
4: section.movie
5: div.movie-container
6: div#app
7: body
8: html
9: document
10: Window {window: Window, self: Window, document: document, name: "", location: Location, …}
length: 11
[[Prototype]]: Array(0)
```
<br>
<br>

**find()메소드 사용하기**


그리고 이렇게 배열이 담긴 cPath 상수에 find 메소드를 적용하는데  
이 **find() 메소드**는 괄호 안에 담긴 조건(함수)에 맞는 요소만 다시 배열로 할당해준다.  

여기서  
cPath의 요소들이 element에 담겨 조건을 확인하게 되는데,  
element의 태그 이름이 "BUTTON"과 같은 요소들만 다시 element라는 상수에 담기게 된다.  

*"BUTTON"은 "button"처럼 소문자가 되면 적용되지 않는다.

```js
const element = cPath.find(element=>element.tagName == "BUTTON")
```

<br>

그리고 **예외처리문**을 사용해 element값이 없으면 아무것도 실행되지 않고 넘어갈 수 있도록 한다.  

```js
if(!element){
    return;
}
```

<br>
<br>

**DOM으로 CSS 클래스 리스트 토글하기**
<br>


이렇게 조건을 다 걸고 나면  
element의 CSS에 클래스를 넣고 뺼 수 있도록 **classList를 이용해 toggle** 될 수 있도록 한다.  

<br>

```css

//css 

.content-favorite button {
    display: flex;
    justify-content: center;
    align-items: center;
    width: 60px;
    height: 60px;
    border: 2px solid #fff;
    border-radius: 100%;
    margin-right: 20px;
}

.button-recommend .icon-thumbs-up {
    width: 23.8px;
    height: 23.8px;
    margin-top: -1px;
    background: center / contain url(../images/icon_thumbs_up.png) no-repeat;
}

.button-recommend.on {
    background-color: #2F80ED;
}

.button-recommend.on .icon-thumbs-up {
    background-image: url(../images/icon_thumbs_up_fill.png);
}

.button-heart .icon-heart {
    width: 22.6px;
    height: 22.6px;
    margin-top: 3px;
    background: center / contain url(../images/icon_heart.png) no-repeat;
}

.button-heart.on{
    background-color: #EB5757;
}

.button-heart.on .icon-heart {
    background-image: url(../images/icon_heart_fill.png);
}

```
<br>

```js
 element.classList.toggle('on');
```
<br>
<br>

**클래스 외부에서 사용할 수 있도록 export하기**
<br>

그리고 Favorite 클래스를 외부에서 사용할 수 있도록 하단에 
`export default Favorite;`를 넣어준다.  
그리고 bindEvents 메소드를 사용할 수 있도록  
`setup()` 메소드를 선언해 `this.bindEvents()`를 실행할 준비를 해준다.  

<br>
<Br>

전체 스크립트 코드는 다음과 같다.  

<br>

```js
//components/index.js


class Favorite {
    constructor(){
        this.favoriteElement = document.querySelector(".content-favorite");
// this는 클래스가 생성한 인스턴스를 가리키고 인스턴스 안에 favoriteElement라는 프로퍼티를 만든다.
// Favorite 객체 { favoriteElement : .content-favorite }
    }

    setup(){
        this.bindEvents();
    }
    // bindEvent()함수를 실행하는 메소드

    bindEvents(){
        // 이벤트 리스너 처리
        this.favoriteElement.addEventListener('click', (event)=>{
            console.log(event.composedPath())
            // 리스너 함수
            const cPath = event.composedPath();
            // composedPath는 이벤트의 경로를 배열값으로 반환한다는 뜻
            // 상수 cPath를 선언하고 event 객체에 composedPath 설정
            // 이벤트 경로란 이벤트가 전파되는 경로

            const element = cPath.find(element => element.tagName == "BUTTON")
            // 배열 cPath에 find 함수를 이용해 find 함수 안에 함수의 조건을 통화한 것만 Element에 담기도록 한다.
            console.log(element)

            if(!element){
                return;
            }
            //조건문으로 예외처리. element가 없으면 return으로 아무것도 실행시키지 않는다.
            element.classList.toggle('on');
            // element가 없으면 그냥 지나가고, element가 있으면 on 클래스를 toggle(있으면 뺴고 없으면 넣음)
        });
    }
}
// 이벤트 위임
// 부모에게 이벤트를 걸어서 이벤트가 아래로 내려가도록


export default Favorite;

```

<br>
<br>

**모듈 전체를 한 곳에 import 하기**

위의 코드를 `js/index.js` 파일에 import 하고  
favorite라는 상수를 선언해 new 연산자로 인스턴스를 생성해준다. 
그리고 내부의 `setup()`메소드를 실행한다.  

<br>
<br>
