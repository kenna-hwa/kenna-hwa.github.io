---
layout: post
title:  "[Javascript] a 태그 스크립트 사용하기"
author: Kenna
date:   2021-07-19 21:26:35 +0830
image: http://hdblackwallpaper.com/wallpaper/2015/07/black-and-white-landscape-photography-1-background-wallpaper.jpg
rating: 42
description: 자바스크립트 공부
categories : Javascript
tags: Javascript
---

###### a 태그에 onclick 등 함수 사용할 때


**void(0) 하고 onclick**
<Br>

```
<a href="javascript:void(0);" onclick="function();">링크 내용</a>
```

**href에 함수 넣기**
<br>

```
<a href="javascript:function();">링크 내용</a>

```
<br>

IE6에서 브라우저 이동 문제가 있을 수 있으니 return false; 추가해주자. (IE6 지원이 이미 끝나서 상관없나..?)  

[참고 페이지]("https://thingsthis.tistory.com/130")