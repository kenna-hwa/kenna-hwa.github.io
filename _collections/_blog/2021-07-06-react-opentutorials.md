---
layout: post
title:  "[React] React - Create 기능구현"
author: Kenna
date:   2021-07-06 23:26:35 +0830
image: https://images.unsplash.com/photo-1593720219276-0b1eacd0aef4?ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&ixlib=rb-1.2.1&auto=format&fit=crop&w=1343&q=80
rating: 38
description: 인프런 - 생활코딩 React 수업
categories : React
tags: React
---

###### React
[Inflearn 생활코딩]("https://www.inflearn.com/course/react-%EC%83%9D%ED%99%9C%EC%BD%94%EB%94%A9/dashboard")


###### 베이스 캠프


state와 props의 차이점<br?

[props vs state]("https://external-content.duckduckgo.com/iu/?u=https%3A%2F%2Fihatetomatoes.net%2Fwp-content%2Fuploads%2F2017%2F08%2F03-state-vs-props-1024x460.png&f=1&nofb=1")

props는 read-only  
state는 `this.setState`로 바꿀 수 있다.  

<br>

**컴포넌트 안에서 자신에게 전달된 props의 값을 바꾸는 것은 금지**
<br>

**컴포넌트 밖에서 props를 바꾸는 것은 허용**

<br>

내부적으로 필요한 데이터나 상태는 state를 통해 관리한다.  
props와 state 모두 render 함수를 호출하기 때문에  
이 두가지를 적절히 사용하여 화면의 UI를 바꿀 수 있다.  

<br>

[state]("https://external-content.duckduckgo.com/iu/?u=https%3A%2F%2Fcodesource.io%2Fwp-content%2Fuploads%2F2020%2F12%2Fstate.jpg&f=1&nofb=1")

사용자의 props와 구현자의 state  
외부에서는 props를 통해서 컴포넌트를 제어한다.  
이 컴포넌트는 props와 state에 따라서 어떤 상태가 될 것인데  
그 상태가 실제 웹 브라우저의 HTML(DOM)에 영향을 줘서 UI가 그려진다.

<br>

**상위 컴포넌트가 하위 컴포넌트에게 값을 전달할때는 props** <br>
**하위 컴포넌트가 상위 컴포넌트에게 값을 전달할때는 Event**


<br>
지금 TOC 컴포넌트에서 글 목록은 어떤 props를 통해 전달하게 될까?
App 컴포넌트가 하위 컴포넌트에게 data라고 하는 props의 값을 전달하는 것.   
<br>

**명령 = props**
<br>

그리고 이벤트가 실행되었을 때 - onclick 같은  
this.setState 함수가 실행되면서 상위 컴포넌트(App)의 상태를 바꿀 수 있다.

[props와 state]("https://external-content.duckduckgo.com/iu/?u=https%3A%2F%2Fmaksimivanov.com%2Fstatic%2F8a0bbd9513656646d76db1f636c06db0%2Fa987b%2Fstate_vs_props.png&f=1&nofb=1")


###### create 구현 : 소개

CRUD  
Create  
Read  
Update  
Delete  

<br>

생성, 수정, 삭제 버튼 만들기  





###### create 구현 : mode 변경 기능



###### create 구현 : mode 전환 기능