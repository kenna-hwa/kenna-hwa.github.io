---
layout: post
title:  "[Javascript] 스크립트를 모듈로 사용하기"
author: Kenna
date:   2021-08-21 14:26:35 +0830
image: https://images.unsplash.com/photo-1579468118864-1b9ea3c0db4a?ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&ixlib=rb-1.2.1&auto=format&fit=crop&w=1350&q=80
description: 제주코딩베이스캠프 파이널코딩테스트 문제 3번
categories : Javascript
tags: Javascript
---
<br>

###### 스크립트 모듈화

<br>

[제코베 파이널코딩테스트 강의](https://www.inflearn.com/course/%ED%94%84%EB%A1%A0%ED%8A%B8%EC%97%94%EB%93%9C-%ED%8C%8C%EC%9D%B4%EB%84%90-%EC%BD%94%EB%94%A9%ED%85%8C%EC%8A%A4%ED%8A%B8/dashboard)
<br><Br>

추천 버튼과 좋아요 버튼을 클릭했을때 각각 내부 아이콘 이미지와 배경색이 변경될 수 있도록 스크립트 작업하기  


여기에서는 모듈화된 스크립트 방식을 사용한다.   
<br>
<br>
  
**모듈화 방식** <br>

모듈화 방식이란 자바스크립트를 여러 개의 파일로 나누어 유지보수와 협력을 수월하게 만들어 주는 방식으로  
한 파일당 하나의 기능 혹은 객체를 담는 컴포넌트를 만들어 사용하는 것을 말한다.  
현재 인터넷 익스플로러에서는 지원하지 않아 표준 측면에서 아쉬운 방법으로  
모바일 브라우저와 마이크로소프트 엣지, 크롬, 사파리, 오페라, 웨일에서는 동작이 가능하다.  

<bR>

모듈을 적용하기 위해 스크립트에 **'module'** 방식을 선언하고 src로 경로를 연결해준다.  
<br>

```html
<script type="module" src="./src/js/index.js"></script>

```
<br>
<br>

**파일 구조**
<br>

하나의 통합된 파일만 연결해주면 되기 때문에 js 폴더에는 components 폴더를 생성한다. 

<br>

```
//폴더구조

src
  |
  |__  js - index.js
        |
        |__components - index.js
```
<br>

js폴더 안의 index.js 파일은 모듈을 한번에 import 시켜 사용하는 최종 파일이고  
components 폴더 안의 파일들은 개별 모듈들로 한 파일당 하나의 객체 혹은 하나의 기능만 담고 있다.  

<br>

```
//js 폴더 내 index.js

import Favorite from "./components/index.js";

const favorite = new Favorite;
// 상수 favorite을 선언하고 new 키워드를 이용해 Favorite클래스의 인스턴스를 생성

favorite.setup();
// Favorite의 인스턴스의 setup 메소드 실행
```

<br>

위와 같이 개별 컴포넌트들을 import로 사용하여 생성자 함수로 인스턴스를 생성해  
인스턴트의 메소드로서 스크립트를 실행한다.  

<br>
<br>