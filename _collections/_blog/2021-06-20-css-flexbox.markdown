---
layout: post
title:  "[CSS] flexbox 이용해서 랜딩페이지 만들기"
author: Kenna
date:   2021-06-20 12:26:35 +0830
image: https://images.unsplash.com/photo-1511140973288-19bf21d7e771?ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&ixlib=rb-1.2.1&auto=format&fit=crop&w=1267&q=80
rating: 28
description: 1분코딩 CSS FLEX 공부
categories : CSS
tags: CSS
---

###### CSS
['1분코딩' CSS Flex]("https://studiomeal.com/archives/197")


###### 샘표SAMPIO

시작은 샘표에서 레시피를 찾다가 홈페이지가 마음에 들어서 랜딩페이지 연습해보기!


<br>

**무드보드Mood Board**
<br>
- 색상   
  
　　포인트 색상 : #ae2223    
　　메인 글자색 : #454545    
　　서브 글자색 : #afa484    
　　라인 색상   : #676566    
　　푸터 바     : #79746e    

<br>

###### flexbox 사용하기

Flex는 Flexible Box, FlexBox라고 부르기도 한다.   
Flex는 레이아웃 배치 전용 기능으로 고안되었다. 그래서 float나 inline-block등을 이용한 기존 방식보다 강력하고 편리한 기능이 많다.   
Flex는 IE10, IE11은 부분 지원된다.   

<br>

###### 부모요소와 자식요소

부모 요소를 플렉스 컨테이너Flex Container 라고 부르고   
자식 요소를 플렉스 아이템Flex Item 이라고 부른다.   
   
**컨테이너가 flex의 영향을 받는 전체 공간이고, 설정된 속성에 따라 각각의 아이템들이 어떤 형태로 배치되는 것**
<br>

<pre>
< div class="container">
	< div class="item">helloflex< /div>
	< div class="item">abc< /div>
	< div class="item">helloflex< /div>
< /div>
</pre>

<br>

###### Flex 컨테이너에 적용하는 속성들



**display: flex;**<br>
컨테이너에 display: flex; 적용하는게 시작!  

flex 아이템들은 가로 방향으로 배치되고, 자신이 가진 내용물의 width 만큼만 차지.   
height는 컨테이너의 높이만큼 늘어난다.   
weight는 내용물만큼 늘어난다.    


**display: inline-flex;**<br>
inline-flex 는 inline-block처럼 동작한다. 컨테이너가 주변 요소들과 어떻게 어우러질지 결정하는 값이다.   


**· 축Axis**
<br>

메인축 : 아이템들이 배치된 방향의 축    
수직축 : 메인축과 수직인 축 (교차축)    

<br>

**· 배치 방향 설정**
<br>

**flex-direction**
<br>

아이템들이 배치되는 축의 방향을 결정하는 속성    
메인축의 방향을 가로로 할건지 세로로 할 건지 정하는 속성  

**flex-direction: row;**<br>
아이템들이 행(가로) 방향으로 배치  


**flex-direction: row-reverse;**<br>
아이템들이 역순으로 가로 배치


**flex-direction: column;**<br>
아이템들이 열(세로) 방향으로 배치


**flex-direction: column-reverse;**<br>
아이템들이 역순으로 세로 배치된다.
<br>
<br>

**· 줄넘김 처리 설정 flex-wrap**
<br>

**flex-wrap: nowrap;**<br>
기본값으로 컨테이너를 넘어가도 줄바꿈을 하지 않음  


**flex-wrap: wrap;**<br>
줄바꿈을 하는데 순차적으로 배치 (튀어나오는 애를 아래로 내림)


**flex-wrap: wrap-reverse;**<br>
줄바꿈을 하는데 역순으로 배치 (튀어나오는 애를 위로 올림!)
<br>
<br>

**· 배치와 줄넘김 한 번에 flex-flow**
<br>

flex-direction과 flex-flow을 한번에 지정할 수 있는 단축 속성으로   
direction, wrap 순으로 한 칸 띄고 사용한다. 
<br>
<br>

**justify**
<Br>
메인축 방향으로 정렬 ↔     

**align**
<br>
수직축 방향으로 정렬 ↕   
<br>


**· 메인축 방향 정렬 justify-content**
<br>
메인축 방향으로 아이템들을 정렬하는 속성  
<br>

**justify-content: flex-start;**
<br>
아이템들을 시작점으로 정렬    
flex-direction이 row(가로) 배치일때는 왼쪽부터   
flex-direction이 column(세로) 배치일때는 위에서 아래로   

**justify-content: flex-end;**
<Br>
아이템들을 끝점으로 정렬    
flex-direction이 row(가로) 배치일때는 오른쪽부터   
flex-direction이 column(세로) 배치일때는 위에서 아래로   

**justify-content: center;**
<Br>
아이템들을 가운데로 정렬    

**justify-content: space-between;**
<Br>
아이템들의 사이between에 균일한 간격

**justify-content: space-around;**
<Br>
아이템들의 둘레around 와 사이between 에 균일한 간격    
따라서 사이에 둘레에 준 간격보다 두 배의 간격이 들어간다.  

**justify-content: space-evenly;**
<Br>
아이템들의 사이와 양 끝에 균일한 간격을 만든다.    
아이템의 둘레와 사이에 모두 균일한 간격을 만들어 준다.  
IE와 엣지는 evenly가 적용되지 않고 around로 적용된다.
<br>
<br>

**· 수직축 방향 정렬 align-items**
<br>
수직축 방향으로 아이템을 정렬하는 속성  

**align-items: stretch;**
<br>
아이템들이 수직축 방향으로 끝까지 늘어난다.  

**align-items: flex-start;**
<br>
아이템들이 시작점으로 정렬한다.  
direction이 row(가로)일 때는 위에서부터,column(세로)일 때는 왼쪽부터.
<br>

**align-items: flex-end;**
<br>
아이템들이 끝점으로 정렬한다.  
direction이 row(가로)일 때는 위에서부터,column(세로)일 때는 왼쪽부터.
<br>

**align-items: center;**
<br>
아이템들을 가운데로 정렬한다.
<br>

**align-items: baseline;**
<br>
아이템들을 텍스트 베이스라인 기준으로 정렬
<br>
<br>

**· 여러 행 정렬 align-content**
<br>
flex-wrap: wrap; 이 설정된 상태에서 아이템들의 행이 2줄 이상 되었을 때의 수직축 방향 정렬을 결정하는 속성
<br>

**align-content: stretch;**
<br>
아이템들이 수직축 방향으로 끝까지 들어난다.  
<br>

**align-content: flex-start;**
<br>
아이템들이 시작점으로 정렬한다.  
direction이 row(가로)일 때는 위에서부터,column(세로)일 때는 왼쪽부터.  


**align-content: flex-end;**
<br>
아이템들이 끝점으로 정렬한다.  
direction이 row(가로)일 때는 위에서부터,column(세로)일 때는 왼쪽부터.
<br>

**align-content: center;**
<br>
아이템들을 가운데로 정렬한다.
<br>

**align-content: baseline;**
<br>
아이템들을 텍스트 베이스라인 기준으로 정렬
<br>
<br>

