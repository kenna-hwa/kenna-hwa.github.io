---
layout: post
title:  "HTTP protocol"
author: Kenna
date:   2021-05-19 22:45:00 +0830
image: http://hdblackwallpaper.com/wallpaper/2015/07/black-and-white-landscape-photography-1-background-wallpaper.jpg
rating: 4
description: MDN 문서
---

###### HTTP 
[MDN 보러가기][https://developer.mozilla.org/ko/docs/Web/HTTP]

**HTTP HyperText Transfer Protocol**
- 하이퍼미디어(데이터 종류에 제약이 없음) 문서를 전송하기 위한 프로토콜
- 클라이언트-서버 모델 : 클라이언트가 요청을 생성하기 위한 연결을 연 다음 응답을 받을 때까지 대기. 수신자 측에 의해 요청이 초기화된다.
- 무상태 프로토콜(Stateless Protocol) : 서버는 요청이 없으면 연결을 유지하지 않는다. 쿠키로 이 문제를 보완할 수 있다.
- TCP/IP 레이어 기반 (TCP/IP : 정보나 파일이일정한 크기의 패킷들로 나뉘어 네트워크 상 수 많은 노드들의 조합으로 생성되는 경로를 거쳐 분산적으로 전송되고, 수신지에 도착한 패킷들이 원래의 정보나 파일로 재조립)
- 웹에서 이루어지는 데이터 교환의 기초
- 현재 http v1.1이 가장 널리 쓰인다.

**요청과 응답**
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

**클라이언트**
클라이언트 : 사용자 에이전트, 브라우저

- 사용자를 대신하여 동작하는 모든 도구
- 항상 요청을 보내는 개체
- 브라우저는 요청을 보내 받은 리소스(문서, 스크립트, 레이아웃 정보, 이미지나 비디오 등)를 혼합하여 사용자에게 표시한다.

**웹 서버**
서버 : 클라이언트의 요청에 대한 문서를 제공하는 단일 기계

