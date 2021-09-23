---
layout: post
title:  "[Javascript] 원시 타입 / 참조 타입 / 원시 래퍼 타입"
author: Kenna
date:   2021-09-23 21:26:35 +0830
image: https://images.unsplash.com/photo-1593720219276-0b1eacd0aef4?ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&ixlib=rb-1.2.1&auto=format&fit=crop&w=1343&q=80
rating: 58
description: 코딩인터뷰를 저격하는 JS 스나이퍼 양성학교 - 원시 타입 / 참조 타입 / 원시 래퍼 타입
categories : Javascript
tags: Javascript
---

###### 원시 타입 / 참조 타입 / 원시 래퍼 타입

**원시 타입**  
<br>

있는 그대로 저장되는 데이터를 표현  

- 불리언  
- 숫자  
- 문자열  
- null  
- undefined  

<br>

원시값을 변수에 할당하면 값이 복사되어 들어간다.  
원시값이 할당된 변수들은 자기 자신의 고유한 값을 가지게 된다.  

<br>

**typeof**  
<br>

원시값의 타입을 알 수 있게 해주는 메서드  
null 타입을 주의.  


```
typeof 변수 or 원시값
```

<br>

**참조 타입**  
<br>

원시 타입을 제외한 타입 전부  
  
변수에 값을 직접 저장하지 않는다.  
변수에는 메모리 안에서 객체를 위치를 가리키는 **포인터** 가 저장된다.   
  
- 객체 : {}  
- 배열 : []  
- 함수  function  
- Date  
- 정규표현식  

<br>


원시 타입도 참조 타입처럼 사용할 수 있다.  

**length, concat 등의 메서드**와 같이 원시 타입을 객체처럼 사용할 수 있도록 해줌

<br>

**오토박싱autoboxing**
<br>
원시 타입을 객체처럼 사용하게 되면 자바스크립트 내부에서 사용하는 데이터의 인스턴스를 만들게 된다.  
이렇게 만들어진 객체는 코드를 실행 후 다음 줄에서 파괴된다.  
이러한 과정을 오토박싱이라고 한다.  

<Br>
<Br>

**총정리**
<br>

- 원시 타입은 불리언,숫자,문자열,null,undefined   
- 참조 타입은 원시 타입을 뺀 나머지  
- 원시 타입은 값 자체가 저장, 참조 타입은 값의 참조 위치가 저장된다.  
- 원시 래퍼 타입은 String, Number, Boolean으로 원시 타입을 객체처럼 사용할 수 있도록 한다.  
