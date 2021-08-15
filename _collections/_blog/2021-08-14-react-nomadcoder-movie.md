---
layout: post
title:  "[React] 필모그래피 영화 앱 만들기 5"
author: Kenna
date:   2021-08-14 20:26:35 +0830
image: https://images.unsplash.com/photo-1591267990439-bc68529677c3?ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&ixlib=rb-1.2.1&auto=format&fit=crop&w=1336&q=80
rating: 51
description: React로 영화 앱 만들기
categories : React
tags: React
---
###### React 생명주기함수 Component Life Cycle

<br>
<br>


리액트는 기본적으로 Component를 생성하고 없애는데 Life Cycle Method를 가진다.  
리액트가 컴포넌트를 생성하고 없애는 주기를 가진다.  

<br>
<br>

**Mounting**
<br>

컴포넌트가 마운팅 될 때(브라우저에 표시될 때) 가장 먼저 호출되는 함수는 
*constructor()*이다. 

construnctor()는 자바스크립트의 class 구조에서 온 함수다.  
그 다음 *render()*가 호출되고 *componentDidMount()*가 호출된다.  
componentDidMount()는 리액트에게 '이 컴포넌트는 처음 렌더링 되었어' 라고 알려준다.  
<br>

순서는  

`=> browser ON`    
  

`constructor()`  
`render()`   
`componentDidMount()`  

순이다. 

<br>
<br>


**Updating**
<br>

업데이트는 사용자가 인터렉션 했을 때 발생한다.  
사용자의 상호작용으로 인해 데이터가 변경되는 경우(setState가 호출되는 경우)    


`=> setState()`


`render()`   
`componentDidUpdate()`  

가 순차적으로 실행된다.  
setState가 호출되면, component를 호출하고, render를 호출한 다음  
업데이트가 완료되면 componentDidUpdate를 실행하는 순서다.  
<br>
<br>

**Unmounting**
<br>
페이지를 이동할 때 컴포넌트는 죽는다.

`componentWillUnmount()`으로 확인할 수 있다.  

<br>
<br>
