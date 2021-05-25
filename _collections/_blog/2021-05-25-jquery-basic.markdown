---
layout: post
title:  "[jQuery] jQuery 기본 선택기"
author: Kenna
date:   2021-05-25 15:26:35 +0830
image: https://images.unsplash.com/photo-1503437313881-503a91226402?ixid=MnwxMjA3fDB8MHxzZWFyY2h8MTR8fGNvZGV8ZW58MHx8MHx8&ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60
rating: 8
description: W3C | jQuery 문서
---

###### 제이쿼리 jQuery
[W3C 공부하러가기]("https://www.w3schools.com/jquery")

###### jQuery 다운로드

- 오프라인에서 사용할 수 있도록 저장

    [jQuery 홈페이지]("http://jquery.com/download")에서 다운로드 가능

    ..js/ 폴더에 저장<br>
    head 태그 안 script 태그에 src 속성에 경로 지정

        <script src="jquery-3.5.1.min.js"></script>

- 공식 CDN 사용

    [jQuery CDN]("https://code.jquery.com")에서 복사한 script 코드를 head 안에 삽입

- 구글 CDN 사용

    head 안에 구글 CDN 코드 삽입
    사용자의 대부분이 구글 CDN의 jQuery를 이미 다운 받았기 때문에 캐시에서 로딩되어 로딩 속도가 빨라진다.

         <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.5.1/jquery.min.js"></script>


###### jQuery 구문

**선택자 Selector**<br>
jQuery 구문은 $달러-()소괄호-""따옴표 가 기본<br>
{ } 중괄호 내부 개행 외에 개행은 안된다.

- $(this).hide() : window, document, this는 ""쌍따옴표 붙이지 않음
- $("p").hide() : element(tag) 선택은 태그 이름
- $(".test").hide() : class 선택자 사용
- $("#test").hide() : id 선택자 사용

→ CSS 선택자와 사용 방법이 같다.

- 추가 선택자 종류

    - $("*") : 모든 element(tag) 선택
    - $("element.className") : element 에서 className 클래스를 가진 태그 선택
    - $("element:first") : element 에서 첫번째 element를 선택
    - $("element li:first-child") : 모든 첫번째 element의 첫번째 li를 선택
    - $("[href]") : 모든 element 중 href 속성을 가진 element를 선택
    - $("element[href='_blank']") : href 속성의 값이 _blank인 element를 선택
    - $("element[href!='_blank']") : href 속성의 값이 _blank가 아닌 element를 선택
    - $(":button") : 모든 button element와 input element 중 button 타입을 가진 element를 선택
    - $("element:even") : element 중 짝수 번째를 선택
    - $("element:odd") : element 중 홀수 번째를 선택

###### jQuery 구문

**ready**<br>
jQuery의 시작은

**$(document).ready(function(){ });**
으로 ready 안에 function() 속 중활호에 { //코드 작성 } 이 기본이다.

위의 ready 코드는

**$(function(){ })**으로 축약 사용이 가능하다.