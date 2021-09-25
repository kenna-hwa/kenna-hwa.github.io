---
layout: post
title:  "[Javascript] call, apply, bind"
author: Kenna
date:   2021-09-24 11:26:35 +0830
image: https://images.unsplash.com/photo-1593720219276-0b1eacd0aef4?ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&ixlib=rb-1.2.1&auto=format&fit=crop&w=1343&q=80
rating: 59
description: 코딩인터뷰를 저격하는 JS 스나이퍼 양성학교 - 좀 더 this 하기 < call, apply, bind >
categories : Javascript
tags: Javascript
---

###### this

<br>

함수를 호출하는 객체  
this를 통해 함수를 다른 객체에서도 글로벌하게 **재사용**할 수 있다.

<br>

일반적으로 this의 값은 자동으로 할당되지만, 상황에 따라 제어할 수 있어야 한다.  

<br>

###### call, apply, bind
**this를 제어하는 함수**

<br>

**call()**<Br>

call 메서드는 this의 값을 바꿀 수도 있고, 함수를 실행할 때 사용할 인수도 전달할 수 있다.

```
menuGlobal.call(참조할 객체, 전달할 인수)
```
<br>


**apply()**<Br>

함수를 실행할 때 인수를 **배열**로 묶어 한번에 전달
<br>

함수의 인자를 여러개 전달하고 인자를 forEach문으로 돌린다.  
이때 forEach에 this를 전달하려면 forEach(function(){}**,this**)처럼 forEach의 두 번째 인자로 this를 선언해야 한다.   
그렇지 않으면  
forEach 안에서 사용한 this는 forEach 내부의 함수를 실행하는 객체를 바라보게 되고 이 객체는 window다.   
window 객체(전역 객체)가 forEach를 부르기 때문.   
두 번재 인자로 선언한 this는 상위 스코프의 객체를 바라보게 된다.  
<br>

<br>

**call()과 apply()의 차이**

<br>

call()은 함수를 실행할 때 전달할 인수를 하나 하나 전달한다면, apply()는 전달할 인수를 배열로 묶어 한번에 전달. 그래서 인수를 두 개만 사용한다.  
인수를 배열로 보낸다는 점 빼고는 call()과 apply()는 동일한 기능을 수행한다.  
<br>


**bind()**<Br>

bind()는 es5에서 추가된 메서드.  
this 값을 어디서 사용하든 호출 객체가 바뀌지 않도록 고정한다.  

<br>

```
function menuGlobal(item){
    console.log("오늘 저녁은 " + item + this.name )
}

var myDinner = {
    name : "김치찌개"
}

var yourDinner = {
    name : "된장찌개"
}

var menuGlobalForMe = menuGlobal.bind(myDinner)
```
<br>


menuGlobalForMe 변수에는 menuGlobal 함수가 바라보는 객체가 myDinner로 고정된 새로운 함수가 들어가게 된다.  
<br>

**화살표 함수와 this**

<br>

화살표 함수의 this는 일반적인 this처럼 함수를 호출한 객체를 할당하지 않고, 바로 상위 스코프의 this를 할당  
forEach의 경우 window 객체를 바라보는데 forEach에도 화살표 함수를 쓰면 상위 스코프의 this를 사용할 수 있다.  
<br>
<br>

- this는 함수를 호출하는 객체를 의미
- call()과 apply()는 this에 할당되는 객체를 지정할 수 있다.  
- bind()는 this에 할당되는 객체가 고정된 새로운 함수를 생성한다.  
- 화살표 함수에서 this는 상위 스코프의 객체를 할당받는다.  