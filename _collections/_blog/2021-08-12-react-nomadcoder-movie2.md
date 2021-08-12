---
layout: post
title:  "[React] 필모그래피 영화 앱 만들기 3"
author: Kenna
date:   2021-08-12 16:26:35 +0830
image: https://images.unsplash.com/photo-1591267990439-bc68529677c3?ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&ixlib=rb-1.2.1&auto=format&fit=crop&w=1336&q=80
rating: 48
description: React로 영화 앱 만들기
categories : React
tags: React
---
###### React로 list의 객체object를 가져오기 => map() 함수
<br>
<br>

<h3>map()</h3>

<br>

map()이 하는 것은 렌더링이다.  
map()은 배열의 각 요소에서 함수를 실행해 그 결과로 배열을 다시 돌려받는다.

<br>


```
const friend = ['a', 'b', 'c', 'd', 'e'];

//old .ver
 
 friend.map(function(arr){
     console.log(arr);
    return arr;
 })

 //arrow function .ver

 friend.map(arr => {
   console.log(arr);
   return arr;
 })

 

/* 
  =>
    a
    b
    c
    d
    e
  (5) ["a", "b", "c", "d", "e"]
*/
```

<br>


지금 const friend = ['a', 'b', 'c', 'd', 'e']; 에 각각 하트를 추가하려면
<br>

```
 friend.map(function(arr){
     return arr+"♥";
 })

 ```

 이렇게 하면  
 ["a♥", "b♥", "c♥", "d♥", "e♥"]  
 이런 결과가 나온다!
  
<br>

<br>

따라서  
map()은 함수를 배열의 모든 아이템에 각각 적용한다.  
그리고 return 값으로 배열을 만들고 배열을 반환한다.  
map()은 배열을 취해 우리가 원하는 배열을 반환해준다.   


<br>

이것을 리액트로 적용해보자.  

음식의 이름과 사진으로 구성된 객체를 아이템으로 가진 배열을 만든다.

<br>

```
const foodList = [
    {
    name : "cake",
    image : "https://images.unsplash.com/photo-1588195538326-c5b1e9f80a1b?ixid=MnwxMjA3fDB8MHxzZWFyY2h8MXx8Y2FrZXxlbnwwfHwwfHw%3D&ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60"
    },
    {
      name : "chocolate",
      image : "https://images.unsplash.com/photo-1511381939415-e44015466834?ixid=MnwxMjA3fDB8MHxzZWFyY2h8MXx8Y2hvY29sYXRlfGVufDB8fDB8fA%3D%3D&ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60"
    },
]
```

<br>

위 배열을 map() 함수를 이용해 각각의 아이템을 반환하도록 하고,  
반환한 값들을 Food 컴포넌트에 넣으면 컴포넌트를 직접 여러개 입력하지 않아도  
map() 함수 덕분에 마치 반복문처럼 컴포넌트를 배열의 아이템 갯수만큼 만들 수 있다.  

<br>

```
foodList.map(item => {
  <Food fav={item.name}/>
}


//item이라는 인자로 foodList의 data를 하나씩 받아온다. 
//받아온 data 중 name이라는 key를 가진 value 값을 item.name으로 받고  
//이 값을 Food 컴포넌트에 props로 전달한다.  


 function Food({ fav }){
  console.log({fav})
  return <h4>I like {fav}</h4>
}
)
```

<br>
<br>


이미지도 동일하게 전달할 수 있다.

<br>

```
function Food({ fav, picture }){
  console.log({fav})
  return <div>
  <h4>I like {fav}</h4> 
  <img src={picture} alt={fav}/>
  </div>
}
```
<br>

My React App is sooooo cooool!!!
<br>

![myapp]("http://kenna.dothome.co.kr/hidden/images/myreactapp.jpg");

<br>
<br>
<br>

###### map() 연습하기

<br>

map()안의 함수를 별도로 빼서 사용할 수 있다.

```
function renderFood(item)){
  console.log(item)
  return <Food name={item.name} picture={item.image} />;
}

function App(){
 return (
   <div>
     <h1>Hello!!!!!</h1>
     {foodIlike.map(renderFood)}
   </div>
 );
}
```

<br>
<br>

그리고 위의 map 함수를 console.log로 받아보면 리액트 컴포넌트의 모양을 볼 수 있다.

<br>

```
(5) [{…}, {…}, {…}, {…}, {…}]
0:
$$typeof: Symbol(react.element)
key: null
props: {name: "kimchi", picture: "https://images.unsplash.com/photo-1583224964978-22…3D&ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60"}
ref: null
type: ƒ Food({ name, picture })
_owner: FiberNode {tag: 0, key: null, stateNode: null, elementType: ƒ, type: ƒ, …}
_store: {validated: false}
_self: undefined
_source: {fileName: "C:\\Users\\peace\\OneDrive\\바탕 화면\\개인공부\\8)노마드코더\\reactmovie-app\\react-movie-2021\\src\\App.js", lineNumber: 37, columnNumber: 10}
[[Prototype]]: Object
1: {$$typeof: Symbol(react.element), key: null, ref: null, props: {…}, type: ƒ, …}
2: {$$typeof: Symbol(react.element), key: null, ref: null, props: {…}, type: ƒ, …}
3: {$$typeof: Symbol(react.element), key: null, ref: null, props: {…}, type: ƒ, …}
4: {$$typeof: Symbol(react.element), key: null, ref: null, props: {…}, type: ƒ, …}
length: 5

```

<br>
<br>
<br>

###### 객체에 key 추가하기

<br>

리액트의 모든 요소는 각각 다르게 보일 필요가 있다.  
리액트는 요소를 알아서 구분할 수 없기 떄문에 key라는 props를 주어야 한다.  
각 객체에 key 라는 이름을 가진 키와 값 한 쌍을 추가한다.  

<br>


```
const foodList = [
    {
    key: 1,
    name : "cake",
    image : "https://images.unsplash.com/photo-1588195538326-c5b1e9f80a1b?ixid=MnwxMjA3fDB8MHxzZWFyY2h8MXx8Y2FrZXxlbnwwfHwwfHw%3D&ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60"
    },
    {
    key: 2,
    name : "chocolate",
    image : "https://images.unsplash.com/photo-1511381939415-e44015466834?ixid=MnwxMjA3fDB8MHxzZWFyY2h8MXx8Y2hvY29sYXRlfGVufDB8fDB8fA%3D%3D&ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60"
    },
]
```
<br>


그리고 값을 전달하고 있는 App 컴포넌트의 Food 컴포넌트에 props를 만들어  
Food 컴포넌트에 key 데이터를 전달한다.

<br>

```
function App(){
 return (
   <div>
     {foodIlike.map(dish => {
       return <Food key={dish.key} name={dish.name} picture={dish.image} />
     })}

   </div>
 );
}
```