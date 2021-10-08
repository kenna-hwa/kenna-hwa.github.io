---
layout: post
title:  "[Javascript] scope"
author: Kenna
date:   2021-09-25 11:26:35 +0830
image: http://hdblackwallpaper.com/wallpaper/2015/07/black-and-white-landscape-photography-1-background-wallpaper.jpg
rating: 60
description: 코딩인터뷰를 저격하는 JS 스나이퍼 양성학교 - 저격수의 소양, < Scope >
categories : Javascript
tags: Javascript
---

###### scope

<br>

**scope유효범위**

<br>

변수의 접근성과 생존 기간을 제어한다.  

스코프는 이름이 충돌하는 문제를 덜어주고, 자동으로 메모리를 관리.  

함수에서 반환하는 순간 함수 스코프 내의 변수들은 해제된다.

<br>

**자바스크립트의 유효범위**

<br>
   
- 전역 스코프   

· 스크립트의 어디서든 접근 가능
· 사용이 쉬움
· 타인과의 협업, 라이브러리 사용 시 충돌 가능성 있음
<br>

- 함수 스코프  

· 함수 내부에서 정의된 변수와 매개변수는 외부에서 접근 불가
· 함수 내부에서 정의된 변수는 함수 내 어디에서든 접근 가능
(자식 함수가 부모 함수의 변수 값에 접근 가능, 그러나 부모 함수에서는 자식 함수의 값에 접근 불가)

```
var func = function(){
    var a = 1;
    var b = 2;
    
    var func2 = function(){
        var b = 5;
        var c = 6;
        
        a = a+b+c;
        
        console.log(a);
    };
    
    func2();
    console.log(c);
}
func();

//첫 번째 콘솔 값은 12
//두 번째 콘솔 값은 Uncaught ReferenceError: c is not defined
```
<br>

*함수 스코프에서의 문제는 함수 스코프 내 변수가 var 등의 키워드로 선언된 변수가 아니면 무조건 전역변수로 인식되어 함수 안의 변수지만 전역변수와 같게 취급한다.  

<br>

- 블록 스코프 (ES6)  

블록 안에서만 존재하는 스코프  

```
if(true){
    var value = "hello";
}
console.log(value);

if(true){
    let value = "world";
}
console.log(value);

//결과 : "hello", "hello"
//let으로 선언한 블록 스코프 내 변수의 경우 외부에서 접근하지 못해 var 으로 선언한 value의 값이 두 번 출력되었다.  
```

<br>


- 스코프는 변수의 접근성과 생존 기간을 제어  
- 이름이 충돌하는 문제를 덜어주고, 메모리를 자동으로 관리  
- 전역 스코프, 함수 스코프, 블록 스코프가 있음  