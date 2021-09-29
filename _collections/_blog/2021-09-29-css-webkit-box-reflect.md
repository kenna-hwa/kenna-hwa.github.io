---
layout: post
title:  "[CSS] -webkit-box-reflect"
author: Kenna
date:   2021-09-29 22:26:35 +0830
image: https://images.unsplash.com/photo-1511140973288-19bf21d7e771?ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&ixlib=rb-1.2.1&auto=format&fit=crop&w=1267&q=80
rating: 61
description: -webkit-box-reflect
categories : CSS
tags: CSS
---

###### -webkit-box-reflect

<br>

이미지나 CSS에 -webkit-box-reflect를 적용하면 거울에 비치는 것 같은 효과를 만들 수 있다.  
현재는 인터넷 익스플로러와 사파리에서는 작동하지 않고 webkit 엔진에서 작동.   

<br>

```css
-webkit-box-reflect : 반사 방향, 원본과 떨어져 있을 거리, 효과
```
<br>

- 반사 방향  
    · above : 원본의 윗 방향으로 반사  
    · below : 원본의 아래 방향으로 반사  
    · left :  원본의 왼쪽 방향으로 반사  
    · right : 원본의 오른쪽 방향으로 반사  

- 원본과의 거리  
    · px, pt, em ...

- 효과  
    · linear-gradient  가 제일 무난하다.

<br>
<br>

```css
-webkit-box-reflect: below 0px linear-gradient(180deg, rgba(#fff, 0) 0%, rgba(#fff, 1), 100%)
```


<br>

참고할 링크  

- https://developer.mozilla.org/en-US/docs/Web/CSS/-webkit-box-reflect
- https://css-tricks.com/state-css-reflections/#webkit-browsers-webkit-box-reflect
