---
layout: post
title:  "[React] 필모그래피 영화 앱 만들기 2"
author: Kenna
date:   2021-08-12 13:26:35 +0830
image: https://images.unsplash.com/photo-1591267990439-bc68529677c3?ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&ixlib=rb-1.2.1&auto=format&fit=crop&w=1336&q=80
rating: 47
description: React로 영화 앱 만들기
categories : React
tags: React
---
###### React 컴포넌트

Component는 HTML을 반환하는 함수다.

<br>

```

function App(){
    return (
        <div>
        <h1>Hello</h1>
        </div>
    )
} export defalut App;

```

<br>

**REACT는 컴포넌트를 이용해서 HTML처럼 작성하려는 경우에 필요하다.**  
컴포넌트를 이용하기 위해서는 index.js에 ReactDOM의 render 함수를 이용해야한다.   

<br>

```
ReactDOM.render(<App />, document.getElementById("root"));
```
<br>

이 부분은 Javascript와 HTML의 조합으로 이 JSX 언어는 React에서만 사용한다.  
컴포넌트의 이름은 반드시 **대문자**로 시작한다. 

<br>
<br>

그리고 사용하기 위해서는 

<br>

```
function App(){
    return (
        <div>
        <h1>Hello</h1>
        </div>
    )
} export defalut App;
//export로 다른 곳에 이 컴포넌트를 사용하겠다고 알리고


// 사용할 컴포넌트에 import 시킨다.
import App from './App';

```
<br>

또한 리액트컴포넌트는   
**단 하나의 컴포넌트만 렌더링** 하기 떄문에  
하나의 컴포넌트로 하위 컴포넌트를 묶어 최상위 컴포넌트만 ReactDOM 렌더 함수에 넣어줘야 한다.
<br>

```
ReactDOM.render(<App /><Potato />, document.getElementById('root')); 
```
<br>

위와 같은 렌더링은 불가능하다.  

그리고 컴포넌트는 한 번 작성해놓으면 다른 곳에서 **재사용이 가능하다.**

<br>
<br>
<br>

###### 상위 컴포넌트가 하위 컴포넌트에게 Props
<br>

```
import React from 'react';

function Food(){
  return <h4>I like potato</h4>
}


function App(){
 return (
   <div>
     <h1>Hello!!!!!</h1>
    <Food fav="kimchi" />

   </div>
 );
}

export default App;
```
<br>


Food 컴포넌트에게 fav 속성(props)를 지정하고 kimchi 라는 값을 줬다.
이 Food 컴포넌트는 위에 만들어둔 하위 컴포넌트다.

이 props에는 다양한 종류의 자료형을 넣을 수 있고  
props를 부모 컴포넌트에서 자식 컴포넌트로 얼마든지 전달할 수 있다.  
누군가 Food 컴포넌트(자식 컴포넌트)로 정보를 보내려고 한다면  
Food 컴포넌트의 인자로 이 props들을 넣는다.   

<br>
<br>
<br>

###### 구조분해할당
<br>

props를 사용하기 위해서는 ES6의 객체 읽기Read 방법인 **props.fav**를 사용할 수 있다.
<br>

```
function Food(props){
  console.log(props.fav) // console => "kimchi"
  return <h4>I like potato</h4>
}
```
<br>

이것을 구조분해할당으로 이용하려면 **{}** 으로 props를 열고 fav를 호출한다.
<br>

```
function Food({ fav }){ //props를 {}로 열고 fav를 호출
  console.log({fav}) //변수처럼 중괄호로 호출한 props의 객체를 사용
  return <h4>I like {fav}</h4> // I like kimchi
}

```

<br>

여기에서 react에서 사용하는 { props.name }은 양쪽에 공백을 사용하고
JSX가 사용하는 {fav}는 양쪽에 공백을 사용하지 않는다.

<br>
<br>
<br>


**=>** 부모 컴포넌트가 자식 컴포넌트에게 data를 보낼때 props를 이용해서 보낸다.  
**=>** props는 컴포넌트에 넣게 되는 data를 말한다.   
**=>** 자식 컴포넌트로 이동한 props는 컴포넌트의 첫번째 인자argument로 간다.  


**1)** props를 호출해서 보내기
<br>

```
function Food(props){
  console.log(props.fav) // console => "kimchi"
  return <h4>I like potato</h4>
}
```
<br>

**2)** props 구조분해 할당해서 보내기
<br>

```
function Food({ fav }){ //props를 {}로 열고 fav를 호출
  console.log({fav}) //변수처럼 중괄호로 호출한 props의 객체를 사용
  return <h4>I like {fav}</h4> // I like kimchi
}

```