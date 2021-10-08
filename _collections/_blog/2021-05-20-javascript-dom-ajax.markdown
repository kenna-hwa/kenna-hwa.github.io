---
layout: post
title:  "[Javascript DOM] Ajax통신의 이해"
author:  Kenna
date:   2021-05-20 23:40:35 +0830
image: https://images.unsplash.com/photo-1601277010173-01291b16774b?ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&ixlib=rb-1.2.1&auto=format&fit=crop&w=1170&q=80
rating: 10
description: 네이버 부스트코스 강의 정리
categories : [DOM]
tags: [DOM]
---


###### Ajax통신의 이해
[부스트코스 강의 보러가기]("https://www.boostcourse.org/web316/lecture/16701/?isDesc=false")


**Ajax**&nbsp;XMLHTTPRequest 통신

웹에서 데이터를 갱신할 때 브라우저 전체를 다시 다운받아 렌더링 하지 않을 수 있는지에 대한 고민에서 시작.

**JSON**&nbsp;JavaScript Object Notation

서버와 클라이언트 사이의 표준적인 데이터 포맷으로 사용



**Ajax 통신의 이해**<br>

- XML, Plain Text, JSON 등 다양한 포맷의 데이터를 주고받을 수 있다. (일반적으로 JSON을 쓴다)

**Ajax 실행 코드**<br>

<pre>
<code>
function ajax(data) {
    var oReq = new XMLHttpRequest();
    oReq.addEventListener("load", function(){
        console.log(this.responseText);
    });
    oReq.open("GET","http://www.example.org/getData?data=data"); //parameter를 붙여서 보낼수있음
    oReq.send();
}
</code>
</pre>




*setTimeout 함수와 비슷하게 동작하는 **비동기로직**

1. XMLHTTPRequest객체를 생성한다.
2. open 메서드로 요청을 준비한다.
3. send 메서드로 서버로 보낸다.
4. 요청 처리가 완료되면(서버에서 응답이 오면) load 이벤트가 발생한다.
5. 콜백함수가 실행된다. 이 시점에서 이미 ajax 함수는 반환되었고 콜스택에서 사라졌다.



------------------------
- CORS 라는 기술은 무엇인가?

    CORS : Cross-Origin Resource Sharing의 줄임말로 '교차 출처 리소스 공유' 라고 해석할 수 있다.

    보안상의 이유로 브라우저는 스크립트가 요청한 교차 출처 HTTP 요청을 제한한다.

    즉, 다른 출처의 응답에 올바른 CORS 헤더가 포함되어 있지 않으면 해당 API를 사용하는 웹 애플리케이션은 애플리케이션이 로드 된 동일한 출처의 리소스만 요청할 수 있다.

![CORS](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS/cors_principle.png)