---
layout: post
title:  "[Javascript DOM] window 객체"
author:  Kenna
date:   2021-05-20 15:20:35 +0830
image: https://external-content.duckduckgo.com/iu/?u=http%3A%2F%2Fcodinghelptech.com%2Fblog_post%2Fdomdocument-object-model-4-638.jpg&f=1&nofb=1
rating: 8
description: 네이버 부스트코스 강의 정리
categories : [DOM]
tags: [DOM]
---


###### Window 객체
[부스트코스 강의 보러가기]("https://www.boostcourse.org/web316/lecture/16698?isDesc=false")


###### setTimeout
window 에는 많은 메서드들이 존재한다.
디폴트의 개념으로 생략할 수 있다.

<pre>
<code>
 window.setTimeout()
 setTimeout()
</code>
</pre>
두 줄의 코드는 같은 뜻이다.

**setTimeout 활용** <br>

setTimeout은 인자로 함수를 받는다. 이 인자로 받은 함수는 나중에 실행되기 때문에 콜백함수라고 한다.

<pre>
<code>
 function run() {
     setTimeout(function() {
         var msg = "hello world";
         console.log(msg)
     }, 1000);
 }

 run()
</code>
</pre>

console.log의 msg는 즉시 실행되지 않고 1000ms(1초) 이후에 실행된다.


**setTimeout의 실행 순서**<br>

setTimeout의 실행은 비동기(asynchronous)로 실행되어 동기적인 다른 실행이 끝나야 실행된다.

<pre>
<code>
function run() {
    console.log("start");
    setTimeout(function() {
        var msg = "hello world";
        console.log(msg); 
    }, 2000);
    console.log("end");
}

run();
</code>
</pre>

위의 코드는 start와 end가 먼저 출력되고 2초 후 hello world가 출력된다.

<pre>
<code>
function run() {
    setTimeout(function() {
        var msg = "hello world";
        console.log(msg);  
    }, 2000);
    console.log("run func end");
}

console.log("start");
run();
console.log("end");
</code>
</pre>

위의 코드는 start -> run func end -> end -> "hello world" 순서로 출력된다.

즉 setTimeout 안의 함수(콜백함수)는 run 함수의 실행이 끝나고 나서 실행된다.
-> stack안에 쌓여 있는 함수의 실행이 끝나고 나서 실행됨


**debugger; 를 통해 스스로 확인하는 것이 좋다.**

<pre>
<code>
function run() {
    setTimeout(function() {
        var msg = "hello world";
        console.log(msg);  
    }, 2000);
    console.log("run func end");
}
debugger;

console.log("start");
debugger;
run();
debugger;
console.log("end");
debugger;
</code>
</pre>




- 추가로 생각해보기

1. 자바스크립트 비동기 예제를 좀 더 찾아보기(setTimeout 말고도 비슷하게 동작하는 것들이 무엇인지 알아보기)


2. setInterval 메서드 알아보기

