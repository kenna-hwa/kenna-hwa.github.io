---
layout: post
title:  "[React] 필모그래피 영화 앱 만들기"
author: Kenna
date:   2021-08-11 13:26:35 +0830
image: https://images.unsplash.com/photo-1593720219276-0b1eacd0aef4?ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&ixlib=rb-1.2.1&auto=format&fit=crop&w=1343&q=80
rating: 46
description: React로 영화 앱 만들기
categories : React
tags: React
---

###### React 로 영화 필모그래피 앱 만들기

1) 주제

- 케이트 블란쳇 배우의 필모그래피를 담은 앱

2) 목적

- API 사용해보기
- 리액트로 앱 제작하기
- 웹 AWS로 배포하기
- SCSS 리액트에 적용하기

3) 내용

- 한국 영화진흥위원회 API를 이용
- 개인적으로 좋아하는 케이트 블란쳇의 필모그래피를 연도별로 나열하고 감상을 기록하기 위해

4) 기능

- 홈
- 네비게이션바 
- 앱 소개
- 배우 소개
- 영화 목록
- 영화 상세 보기
- 티저 영상
- 댓글을 달 수 있는 비동기 기능 (디스코드 등)
- 방문자수

<br>


**처음으로 시작하는 토이프로젝트로 시간이 많이 걸리는 디자인 부분을 최소화하여 프로그래밍 부분을 공부하는데 집중하고**    
**배포까지 스스로 도전해보는 프로젝트**  


<br>

노마드 코더의 < 클론코딩 영화 평점 웹서비스 > 를 기반으로  
리액트 앱을 구성하고   
CSS는 SCSS를 이용하여 개발할 계획이다.


<br>

###### REACT 란?

내가 사용하려고 하는 리액트는 자바스크립트의 라이브러리로  
페이스북에서 개발한 UI를 위한 라이브러리이다.  

리액트는    
- 선언적 Declarative  
- 컴포넌트 기반 Component-Based  
- 한 번 배우면 어디에서나 쓸 수 있음 Learn Once, Write Anywhere  
과 같은 특징을 가지고 있다.   


<br>

**선언적 Declarative**

<br>
직관적이고 어플리케이션에서 사용하는 상태 정보들을 State와 Props로 쉽게 다룰 수 있도록 한다.  

![props/state](https://external-content.duckduckgo.com/iu/?u=https%3A%2F%2Fcodetoart.com%2Frails%2Factive_storage%2Fblobs%2FeyJfcmFpbHMiOnsibWVzc2FnZSI6IkJBaHBRdz09IiwiZXhwIjpudWxsLCJwdXIiOiJibG9iX2lkIn19--87501a1873d22267e89b7a881c6a7ee545473486%2Fpic-2.png&f=1&nofb=1)

<br>

**컴포넌트 기반 Component-Based**
<br>

객체지향언어인 자바스크립트와 닮은 JSX라는 언어를 사용하고 있으며  
class나 function으로 선언하는 컴포넌트를 기반으로 한다.  
이 컴포넌트를 조합해 사용자가 사용하는 화면을 구성하고  
props와 state를 사용해 사용자가 전달하는 값을 내부에서 구현할 수 있다.

<br>


**한 번 배우면 어디에서나 쓸 수 있음 Learn Once, Write Anywhere**
<br>

리액트는 리액트 네이티브 React Native라는 언어로 전환이 가능하며 Node.js를 통해 서버에 업데이트 할 수도 있다.

<br>

특히 리액트는 가상의 돔 Virtual DOM 을 구성하는데,  
DOM은 브라우저가 화면을 그리기 위한 정보를 가진 문서고  
브라우저가 화면을 렌더링 할 때 정보가 바뀌면 화면 전체를 다시 그려야하는 비효율성을 바꾸기 위해 버추얼돔을 사용한다.  
<br>


리액트는 컴포넌트가 렌더 함수를 호출하여 브라우저에 렌더링을 하는데    
렌더 함수가 호출되자마자 브라우저에 HTML 코드를 넣는 것이 아니고   

버추얼돔을 먼저 구성하고, 실제 브라우저의 DOM과 비교하여 달라진 부분만을 렌더링 하여 훨씬 빠른 개발을 할 수 있도록 도와준다.  

<br>

![reactVirtualDOM]("http://kenna.dothome.co.kr/hidden/images/blog_react_1.jpg")

<br>



내가 리액트를 배우는 궁극적인 목표는  
국내외 회사에서 리액트를 웹서비스에 사용하고 있어 취업을 위해서기도 하지만  
나중에 **모바일 앱**을 만들어보려고도 하기 때문이다.  
앞으로는 리액트를 이용한 다양한 앱을 클론코딩하고 변형해서 다양한 토이프로젝트를 진행해보려고 한다.  
