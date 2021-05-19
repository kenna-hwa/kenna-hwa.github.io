---
layout: post
title:  "HTTP protocol"
author: Kenna
date:   2021-05-19 22:45:00 +0830
image: http://hdblackwallpaper.com/wallpaper/2015/07/black-and-white-landscape-photography-1-background-wallpaper.jpg
rating: 4
description: MDN 문서 HTTP 개요
---

###### HTTP 
[MDN 보러가기]("https://developer.mozilla.org/ko/docs/Web/HTTP")

**HTTP HyperText Transfer Protocol**
- 하이퍼미디어(데이터 종류에 제약이 없음) 문서를 전송하기 위한 프로토콜
- 클라이언트-서버 모델 : 클라이언트가 요청을 생성하기 위한 연결을 연 다음 응답을 받을 때까지 대기. 수신자 측에 의해 요청이 초기화된다.
- 무상태 프로토콜(Stateless Protocol) : 서버는 요청이 없으면 연결을 유지하지 않는다. 쿠키로 이 문제를 보완할 수 있다.
- TCP/IP 레이어 기반 (TCP/IP : 정보나 파일이일정한 크기의 패킷들로 나뉘어 네트워크 상 수 많은 노드들의 조합으로 생성되는 경로를 거쳐 분산적으로 전송되고, 수신지에 도착한 패킷들이 원래의 정보나 파일로 재조립)
- 웹에서 이루어지는 데이터 교환의 기초
- 현재 http v1.1이 가장 널리 쓰인다.

**요청과 응답**<br>
![클라이언트-프록시-프록시-서버](https://mdn.mozillademos.org/files/13679/Client-server-chain.png)
1. 클라이언트의 개별적인 요청
2. 서버로 보내짐
3. 서버는 받은 요청을 처리
4. response 응답을 클라이언트로 보냄

각각의 개별적인 요청을 처리하는 클라이언트와 서버 사이에는 여러 개체가 있다.
- 게이트웨이
- 프록시
       - 컴퓨터/머신 중 애플리케이션 계층에서 동작
       - 캐싱 (캐시는 공개 또는 비공개가 될 수 있다.)
       - 필터링 (바이러스 백신 스캔, 유해 컨텐츠 차단)
       - 로드 밸런싱 (여러 서버들이 서로 다른 요청을 처리하도록 허용)
       - 인증
       - 로깅
- 라우터
- 모뎀

**클라이언트**<br>
사용자 에이전트, 브라우저

- 사용자를 대신하여 동작하는 모든 도구
- 항상 요청을 보내는 개체
- 브라우저는 요청을 보내 받은 리소스(문서, 스크립트, 레이아웃 정보, 이미지나 비디오 등)를 혼합하여 사용자에게 표시한다.

**웹 서버**<br>
클라이언트의 요청에 대한 문서를 제공하는 단일 기계

###### HTTP 흐름

클라이언트가 서버와 통신하고자 할 때 다음 과정을 수행한다.

1. TCP 연결을 연다.
       TCP 연결은 요청을 보내거나 응답을 받는데 사용된다. 클라이언트는 새 연결을 열거나, 기존 연결을 재사용하거나, 여러 개의 연결을 열 수 있다.

2. HTTP 메시지를 전송한다.
       HTTP는 인간이 읽을 수 있다. HTTPv2는 간단한 메시지가 프레임 속으로 들어가 직접 읽는 것은 불가능 하다.

3. 서버에 의해 전송된 응답Response을 읽어들인다.
       
4. 연결을 닫거나 다른 요청들을 위해 재사용한다.
           
**요청 메시지 포맷**<br>
- 요청 메서드<br>
       - GET : 정보를 요청하기 위해 사용. SELECT. 요청 바디가 없다.<br>
       - POST : 정보를 밀어넣기 위해 사용. INSET. 요청 바디가 있다.<br>
       - PUT : 정보를 업데이트 하기 위해 사용. UPDATE. 요청 바디가 있다.<br>
       - DELETE : 정보를 삭제하기 위해 사용. DELETE<br>
       - HEAD : HTTP의 헤더 정보만 요청. 해당 자원이 존재하는지 혹은 서버에 문제가 없는지 확인하기 위해 사용.<br>
       - OPTIONS : 웹 서버가 지원하는 메서드의 종류를 요청.<br>
       - TRACE : 클라이언트의 요청을 그대로 반환. echo 서비스로 서버 상태를 확인하기 위해 주로 사용.<br>
- 요청 URL : 가져오려는 리소스의 경로
- HTTP 버전
- 빈 줄
- 요청 바디<br>
![Method, Path, Version of the protocol, Headers](https://mdn.mozillademos.org/files/13687/HTTP_Request.png)


**응답 데이터 포맷**<br>
- 응답 헤더<br>
       - 응답 HTTP 프로토콜의 버전<br>
       - 응답 코드<br>
       - 응답 메시지<br>
       - 날짜<br>
       - 웹서버 이름과 버전<br>
       - 콘텐츠 타입<br>
       - 캐시 제어 방식<br>
       - 콘텐츠 길이<br>
- 빈 줄
- 응답 바디
- 실제 응답 리소스 데이터<br>
![Version of the protocol, Status code, Status message, Header](https://mdn.mozillademos.org/files/13691/HTTP_Response.png)



###### HTTP 메시지

초기 HTTP와 HTTPv1.1의 메시지는 사람이 읽을 수 있었으나 HTTPv2에서는 프레임 안에 임베드 되어 최적화된다.<br>
그러나 각 메세지들의 의미는 변하지 않으며 클라이언트는 본래의 HTTPv1.1 요청을 가상으로 재구성한다. 


###### HTTP 기반 API

보편적으로 HTTP 기반으로 사용되는 API는 **XMLHttpRequest API**이다.
그리고 최신 Fetch API는 보다 강력하고 유연한 기능을 제공한다.

서버-전송 이벤트는 서버가 전송 매커니즘으로 HTTP를 사용하여 클라이언트로 이벤트를 보낼 수 있도록 하는 단방향 서비스다. 
클라이언트는 EventSource 인터페이스를 사용하여 연결을 맺고 이벤트 핸들러를 설정한다.

브라우저는 HTTP스트림으로 도착한 메세지를 적절한 Event객체로 자동 변환하여 이벤트 핸들러로 전달하거나 특정 유형의 이벤트가 생성되지 않은 경우에는 onmessage 이벤트 핸들러로 전달한다.


###### 결론

HTTP는 사용이 쉬운 확장 가능한 프로토콜로 클라이언트-서버 구조는 HTTP가 웹의 확장된 수용 능력과 함께 발전하도록 만들어주고 있다.


