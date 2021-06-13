---
layout: post
title:  "[HTML] 상태정보/Cookies/Session"
author: Kenna
date:   2021-06-13 09:26:35 +0830
image: https://images.unsplash.com/photo-1592825508076-d59e805443cc?ixid=MnwxMjA3fDB8MHxzZWFyY2h8OTh8fGNvb2tpZXN8ZW58MHx8MHx8&ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60
rating: 21
description: 네이버 부스트코스 강의 정리
categories : HTML
tags: HTML
---

###### 쿠키Cookie와 세션Session
[부스트코스 강의 보러가기]("https://www.boostcourse.org/web316/lecture/16798")  
[참고한 블로그 글]("https://jaejade.tistory.com/42")


###### 웹Web 에서의 상태 유지 기술

- 기본 HTTP 프로토콜은 상태 유지가 안되는 프로토콜이다.  
- 클라이언트에 대해 서버는 클라이언트가 이전에 무엇을 했고, 지금은 무엇을 했는지에 대한 정보값을 가지고 있지 않다.  
- 웹 브라우저(클라이언트)의 요청에 대한 응답을 하고 나면 해당 클라이언트와의 연결을 지속하지 않는다.  
<br>


**→ 이것을 해결하기 의해 쿠키Cookie와 세션Session 기술이 등장한다.**
<br>
앞선 클라이언트가 로그인했는지, 장바구니에 뭘 넣었는지 알게 하고 이런 것들을 유지하기 위해
클라이언트가 두 번째, 세 번째 요청을 했을 때 이 클라이언트가 어떤 사용자인지 기억하게 하는 기술.
<br>
<br>

###### 쿠키Cookie와 세션Session

- **쿠키Cookie** 
    사용자 컴퓨터에 저장  
    유효기간이 지나면 사라짐  
    세션보다 처리 속도가 빠름  
    저장된 정보를 다른 사람 또는 시스템이 볼 수 있음(단점)  

<br>

- **세션Session**
    서버에 저장  
    서버가 종료(브라우저가 종료)되거나 유효시간이 지나면 사라지기 떄문에 보안이 좋음  
    세션키로 통신해 네트워크 부하가 낮음  
    서버에 저장하기 때문에 데이터가 늘어면 그때 부하가 생김(단점)   
    브라우저가 아닌 서버에서 처리하기 때문에 쿠키보다 속도가 느림(단점)   
    쿠키와 마찬가지로 중간에 노출 될 수 있음(단점)   
<br><br>
<br>

###### 쿠키Cookie와 세션Session 의 동작 이해 
<br>
<br>
<br>

**쿠키의 동작 이해**
<br>
<br>

<img src="https://cphinf.pstatic.net/mooc/20180221_5/1519187850598AmEe1_PNG/1.png" width="600px"/>  
<br>
<br>

1) 클라이언트가 서버 쪽에 요청을 보낸다.  
2) 요청 중에 유지해야 될 정보가 있다면 서버는 유지할 정보를 가지고 쿠키 **Set-Cookie header**를 생성한다.   
3) 서버가 만든 쿠키는 **반드시 응답 결과에 포함** 되어서 클라이언트에게 보내져야 한다. 이 때 클라이언트(웹 브라우저)는 이를 저장해놓는다. 
<br>

**→ 만들어진 쿠키는 클라이언트가 가지고 있게 된다.**
<br>
<br>
  
<img src="https://cphinf.pstatic.net/mooc/20180221_188/1519187853247UDkY0_PNG/2.png" width="600px"/>    
<br>
<br>

4) 클라이언트는 앞으로 요청할 때 이 쿠키**Set-Cookie header**를 같이 포함시켜서 서버에게 보낸다.    
5) 서버는 이 쿠키가 존재하는지 검사하고 있으면 어떤 클라이언트가 요청했고 유지되야 하는 이전 정보가 있는지 알아낸다.    
+Expires 혹은 Max-Age를 설정하면 명시된 기간까지 쿠키가 유지된다.  
<br>
<br>
 

**세션의 동작 이해**<br>
<br>
<br>
  
<img src="https://cphinf.pstatic.net/mooc/20180221_246/15191878577834bPNF_PNG/3.png" width="600px"/>    
<br>
<br>
 
 1) 클라이언트가 서버 쪽에 요청을 보낸다. 
 2) 요청 중에 유지해야 될 정보가 있다면 서버는 세션키를 만들어낸다.  
 3) 그리고 세션키를 이용한 저장소를 생성한다. **Session Storage** 여기에 저장해야 하는 정보를 저장하게 된다.  
 4) 추후 요청 시 해당 클라이언트의 세션 저장소를 알아내기 위해 세션키를 담은 쿠키**Set-Cookie header**를 만든다.  
 5) 이 쿠키를 응답 결과에 포함해 클라이언트에게 보낸다.  
<br>
<br>

   
<img src="https://cphinf.pstatic.net/mooc/20180221_236/15191878600705qUuz_PNG/4.png" width="600px"/>     
<br>
<br>

6) 이 클라이언트가 다시 서버에 무언가를 요청할 때는 세션키를 저장한 쿠키**Set-Cookie header**를 포함해서 요청을 보낸다.  
7) 서버는 받은 세션키를 활용해 이전의 저장소를 찾아 정보를 활용한다.  
    이 저장소에 들어있는 정보를 사용, 저장소에 다시 원하는 정보를 저장하는 일을 수행하고  
    이때 세션의 정보를 담기 위해 생성되는 객체가 **HttpSession**이다.  
<br>
<br>
<br>

###### + 토큰 Token 이란?
<br>
<br>

쿠키와 세션의 단점을 보완하기 위해 토큰Token이 등장
<br>
<br>
<img src="https://images.unsplash.com/photo-1533988902751-0fad628013cb?ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&ixlib=rb-1.2.1&auto=format&fit=crop&w=1051&q=80" width="500px"/>  

<br>

1) 클라이언트가 로그인을 하면 서버는 해당 클라이언트에 대한 계정 정보를 확인  
2) 클라이언트가 확인되면 (로그인을 하거나) 서버는 **signed token**을 발급한다.  
3) 클라이언트는 발급 받은 signed token을 저장한다.  
4) 이후 요청을 보낼 때 마다 저장해준 이 token을 **HTTP header**에 담아 보낸다.  
5) 서버는 token을 검증하고 클라이언트의 요청에 응답한다.  
<br>

이 헤더에 담겨온 토큰을 검증하는 과정은 무상태성 Stateless를 가진다.  
정보가 담긴 데이터를 암호화하여 HTTP header에 담아 전달하기 때문에 쿠키를 사용할 때처럼 보안에 취약하지는 않지만 token도 탈취될 수 있다.   

토큰 기반 인증 방식 중 가장 많이 사용되는 것은 **JWT JSON Web Token** 으로 무결성을 보장하기 때문에 위조된 토큰인 경우 바로 알아낼 수 있다.   

**OAuth**를 통해 다른 서비스 계정(google, facebook 등)으로 로그인 할 수 있고, 선택적 권한만 부여할 수 있다.  
<br>
<br>

###### + HTTP 프로토콜의 특징 
<br>

HTML의 특징은 **무연결성 Connectionless** 과 **무상태성 Stateless** 이다.  

- **무연결성 Connectionless** : 클라이언트가 서버에게 요청과 응답을 보내고 받는 과정은  연결 수립 - 요청 - 응답 - 연결 종료 순으로 진행된다.   
Http 프로토콜은 이러한 과정이 끝나면 연결을 종료한다.   

- **무상태성 Stateless** : http 프로토콜은 독립적인 과정으로 진행된다.   
서버는 클라이언트가 이전에 어떤 상태였는지 알지 못한다.    
<br>

이 두 가지의 특징은 불특정 다수를 대상으로 하는 서비스에 적합하다.   
클라이언트-서버 연결 수 보다 많은 요청과 응답을 처리할 수 있기 때문이다.   
하지만 무연결성 때문에 클라이언트의 이전 상황을 서버는 알 수 없다.   
이를 보완하기 위해 쿠키Cookie와 세션Session 기술이 생겼다.   
<br>
<Br>

###### + 상태가 유지되는 프로토콜에는 어떤 것이 있을까?  
<br>

프로토콜은 **상태 Stateful** / **무상태 Stateless** 로 나뉜다.  
<br>

- **상태유지 Stateful 프로토콜**  
    
클라이언트가 서버에 요청을 보내면 어떤 종류의 응답을 기대하고 응답이 없으면 요청을 다시 보낸다.   
현재 상태와 세션 정보를 유지하기 위해 별도로 저장들 위한 서버가 필요하다.    
서버와 클라이언트는 서로 밀접하게 관계된다.    
서버는 세션 정보 및 기타 세부 정보를 유지해야 해 충돌 관리가 어렵다.     
트랜잭션 처리가 비교적 느리다.   
<br>

**FTP, Telnet**
<br>
<br>

- **무상태 Stateless 프로토콜**
<br>

클라이언트가 서버에 요청을 보내고 주어진 상태에 따라 서버 응답을 보낸다.    
서버 정보 또는 세션 정보를 저장하지 않아 별도로 저장들 위한 서버가 필요하지 않다.    
서버와 클라이언트는 독립적이다.    
서버는 세션 정보와 기타 세부 정보를 저장할 필요 없고 충돌이 발생하면 바로 다시 시작할 수 있다.   
트랜잭션을 빠르게 처리한다.    
<br>

**HTTP, UDP, DNS**

[참고한 블로그 글]("https://www.tutorialspoint.com/difference-between-stateless-and-stateful-protocols")

